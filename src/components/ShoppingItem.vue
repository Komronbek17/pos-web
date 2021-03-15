<template>
    <div class="outline">
        <!-- Container -->
        <div class="container"> 
            <img :src="item.avatar" :alt="item.model">
            
            <div :class="{ hide:showCart }">
                <div class="property">Model : {{item.model}}</div>
                <div class="property">Price : {{item.price}} $</div>
                
                <div class="btn-container">
                    <div class="btn"
                        :class="{'picked-cart':pickedCart}" 
                        @click="addToCart(item.id)"
                    >
                        {{btnText}}
                    </div>
                    <div class="btn" 
                        style="background:#FDD935"
                        @click=" showCart = true "
                    >
                        Quick view
                    </div>
                </div>
            </div>

            <div class="add-to-cart" v-if="showCart" :class="{'active-cart':showCart}">
                <div>RAM : {{item.RAM}}</div>
                <div>
                    Internal Memory : {{item.internalMemory}}
                </div>
                <div>Rear Camera : {{item.rearCamera}}</div>
                <div>
                    Front Camera : {{item.frontCamera}}
                </div>
                <div>
                    Screen Size ( in cm ) : {{item.screenSize}}
                </div> 

                <div class="btn btn-back" 
                    @click=" showCart = false "
                >
                    Back
                </div>
            </div>
        </div>
        <!-- End Of Container -->
    </div>
</template>

<script>
    export default {
        props:['item','cartActive'],
        watch:{
            cartActive(last){
                if(this.item.id ==last.id){
                    this.pickedCart = last.logic;
                };
            }
        },
        data() {
            return {
                showCart:false,
                btnText:'Add to Cart',
                pickedCart:null
            }
        },
        methods: {
            addToCart(id){
                this.$emit('addToCart',id);
                this.btnText="Added to Cart";
                this.pickedCart = true ;
            },
        },
    }
</script>

<style lang="scss" scoped>
.hide{
    opacity: 0;
    color:white;
}

img{
    width:150px;
    background-color: #f4f4f4;
}

.container{
    border-right: 1px solid #361999;
    border-bottom: 1px solid #361999;
    margin:1rem;
    background: white;
    box-shadow: 0 0 3px black;
    display: flex;
    justify-content: center;
    align-items: center;
    padding:1rem;
    white-space: nowrap;
    position: relative;
    width:25rem;
    height: 15rem;
    text-align: center;
    transition: all 0.5s;

    &:hover{
        box-shadow: 0 0 9px #361999;
    }

    @media screen and (max-width:1300px){
        &{
            margin:0.5rem;
            padding:0.5rem;
            width: 20rem;
            height: 10rem;

            img{
                width: 100px;
            }
        }
    }

    @media screen and (max-width:1100px){
        &{
            margin:0.5rem;
            padding:0.5rem;
            width: 20rem;
            height: 10rem;
            font-size:1rem;

            img{
                width: 100px;
            }

            .btn{
                margin-top:0.5rem;
                padding:.2rem;  
            }
        }
    }

     @media screen and (max-width:1065px){                                       
        &{
            margin:1rem;
            padding:1rem;
            width: 25rem;
            height: 15rem;

            img{
                width: 200px;
            }

            .btn{
                margin-top:1rem;
                padding:.5rem;  
            }
        }
    }
}

.property{
    margin:1rem 0;
    text-transform: capitalize;
    font-weight: 800;
}

.add-to-cart{
    position:absolute;
    bottom:0;
    left:0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.7);
    color:whitesmoke;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    transition: all 0.5s;
    text-align: right;

    div{
        margin: 0.3rem 0;
    }
}

/* Button */
.btn{
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
    padding-top: 10px;
    padding:0.3rem;
    font-family: monospace;
    font-size: 1rem;
    cursor: pointer;
    text-align: center;
    transition: all .5s;
    z-index: 2;
    background: #1FC58E;
    font-weight: 500;
    margin-top: 1rem;
    position: relative;
    color: black;

    &::before{
        content: '';
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        z-index: -1;
        bottom:0;
        left:0;
        width: 0;
        height: 9%;
        background: #361999;
        transition: all .5s;
    }

    &:hover{
        &::before{
            width: 100%;
        }
    }
}
.btn-back{
    padding:0.2rem 0.7rem;
    position: absolute;
    bottom:2%;
    right: 2%;
}

.picked-cart{
    background:#4E3883;
    color: rgb(255, 244, 89);
    cursor:context-menu;
}

@media screen and (max-width:800px) {
    *{
        font-size: 0.8rem;
    }

    .container{
        margin:0.5rem;
        padding:0.5rem;
        width: 20rem;
        height: 10rem;
        font-size:1rem;

        .btn{
            margin-top:0.5rem;
            padding:.2rem;  
        } 
    }

    .container img{
        width:150px;
    }
}

@media screen and (max-width:650px) {
    *{
        font-size: 0.7rem;
    }

    .container {
        width:100%;
        height: 50%;
    }

    .container img{
        width: 100px;
    }
}

@media screen and (max-width:550px) {
    *{
        font-size: 0.5rem;
    }

    .container .btn {
        font-size: 0.5rem;
    }

    .container img{
        width: 80px;
    }
}
</style>