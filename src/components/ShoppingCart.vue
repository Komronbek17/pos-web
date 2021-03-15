<template>
    <div class="cart-container">
        <div class="title">
            <h2>#Cart</h2>
        </div>
        <div class="selected-carts">
            <div class="shopping-cart"
            v-for="item in selectingItems"
            :key="item.id"
            >
                    <SingleCart 
                        :item="item" 
                        @deleteItem="deleteItem(item)"
                        @totalPrice="totalyPrice" 
                    />
            </div>
        </div>    
        <!-- Result -->
        <div class="total-price">
            Total Price : <span style="color:yellow">{{ wholePrice() }}$</span>
            <div>
                <button class="pay-btn">Pay</button>
            </div>
        </div>
    </div>
</template>

<script>
    import SingleCart from './SingleCart.vue';
    export default {
        emits:['deleteItem','totalPrice'],
        data() {
            return {
                sumArray: []
            }
        },
        props:{
            selectingItems:Array,
        },
        components:{
            SingleCart
        },
        methods: {
            deleteItem(item){
                this.$emit('deleteItem',item.id);
                const index = this.findIndex(item);
                this.sumArray.splice(index,1);
                this.wholePrice();
            },

            totalyPrice(item){
                if(this.sumArray.length !== 0){
                    const hasItem = this.sumArray.find(obj => obj.id == item.id)
                    
                    if(hasItem){
                        const index = this.findIndex(hasItem);
                        this.sumArray[index].sum = item.sum;
                    }
                    else{
                        this.sumArray.push(item);
                    }
                }
                else {
                    this.sumArray.push(item);
                }

                
                this.wholePrice();
            },

            findIndex(item){
                const index = this.sumArray.findIndex(obj => obj.id == item.id);

                return index;
            },

            wholePrice(){
                let total = 0;
                if(this.sumArray.length>0){
                    const summa = this.sumArray;
                    for(let item = 0; item<summa.length;item++){
                        total+=summa[item].sum;
                    }
                    
                }
                
                return Number.parseFloat(total).toFixed(2);
            }
        },
    }
</script>

<style lang="scss" scoped>
.cart-container{
    position:fixed;
    top:0;
    right:0;
    width:29%;
    height: 100vh;
    overflow-y: scroll;
    background: rgba( #fff, 0.7);
    padding: 1rem;

    @media screen and (max-width:1100px){
        &{
            width:40%;
        }
    }

    .title{
        color: #161F6D;
        text-align: center;
        margin-top: 0.5rem;
        letter-spacing: 2px;
        font-family: monospace;
    }
}

.total-price{
    position: absolute;
    bottom:0;
    width:90%;
    height: auto;
    background:#51b48b;
    color: whitesmoke;
    font-weight: 800;
    margin: 0.5rem 0;
    text-align: center;
    white-space: nowrap;
    font-size: 1.5rem;

    @media screen and (max-width:700px){
        &{
            font-size: 1rem;
        }
    }

    @media screen and (max-width:500px){
        &{
            font-size: 0.7rem;
        }
    }

    div{
        text-align: right;
    }
}

.pay-btn{
   width: auto;
   padding: 0.1rem 0.8rem;
   margin-bottom: 0.5rem; 
   margin-right: 0.5rem;
   background: whitesmoke;
   color:black;
   font-size: 1.2rem;
   border: none;
   outline: none;
   border-radius: 5px;
   transition: all 0.5s;

    @media screen and (max-width:700px){
        &{
            font-size: 1rem;
            padding: 0.1rem 0.4rem;
        }
    }
    @media screen and (max-width:500px){
        &{
            font-size: 0.7rem;
        }
    }

   &:hover{
    background: #44449B;
    color: whitesmoke;
   }

   &:active{
    transform: scale(0.9);
   }
}

</style>