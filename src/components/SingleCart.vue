<template>

    <div class="cart-item">
        <h3 class="model">Name: {{item.model}}</h3>
        <div class="flex-position">
            <div class="delete-btn" @click="$emit('deleteItem')">
            <i class="fas fa-trash"></i>
            </div>
            <div class="default-price">
                <p>{{shortening(item.price)}} $ </p>
            </div>
        </div>
        
        <div class="right-angle">
            <div class="selected-price">
                <span>{{shortening(item.price*counter)}} $</span>
            </div>
            <div class="manage-items">
                <span>
                    <i class="fas fa-chevron-up" @click="changeCounter(1)"></i>
                </span>
                <span class="item-numbers">
                    {{counter}}
                </span>
                <span @click="changeCounter(-1)">
                    <i class="fas fa-chevron-down"></i>
                </span>
            </div>
        </div>
    </div>
    
</template>

<script>
    import { ref } from 'vue';
    export default {
        props:['item'],
        /* SETUP */
        setup(props,context) {
            let counter = ref(1);
                
            let sum = ref(counter.value * props.item.price); 

            context.emit('totalPrice',{
                id:props.item.id,
                sum:sum.value
            });

            function changeCounter(incDec){
                if(counter.value == 1 && incDec < 0){
                    context.emit('deleteItem');
                    counter.value = 0;
                }

                if(counter.value > 1 || incDec > 0){
                    counter.value += incDec;
                }

                sum.value = counter.value * props.item.price;
                context.emit('totalPrice',{
                    id:props.item.id,
                    sum:sum.value
                });
            }

            function shortening(number){
                return Number.parseFloat(number).toFixed(2);
            }
                
            

            return {
                counter,
                changeCounter,
                shortening
            }
        }
    }
</script>

<style lang="scss" scoped>

.animate__animated.animate__fadeInUp {
  --animate-duration: 10s;
}

.cart-item{
    user-select: none;
    height: 5rem;
    width:100%;
    background: #E1E2E2;
    color: black;
    padding-bottom: 2rem;
    margin-bottom: 0.1rem;
    position: relative;
    border-left: 2px solid #41B883;

    .model{
        text-transform: capitalize;
        margin:0.1rem;
        margin-bottom: 0.6rem;
        padding-top: 1rem;
        color: #000000;
    }
}

.flex-position{
    display: flex;
}

.delete-btn{
    color: red;
    margin-left: 1rem;
    margin-right: 1rem;
}

.right-angle{
    position: absolute;
    right: 1%;
    top:1%;
    display:flex;
    text-align: center;

}

.manage-items{
    display:flex;
    flex-direction: column;
    margin:1rem;
    margin-left: 0;
}

.selected-price{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-right: 2rem;
}

@media screen and (max-width:900px) {
    *{
        font-size: 0.8rem;
    }
}

@media screen and (max-width:560px) {
    *{
        font-size: 0.5rem;
    }

    .cart-item{
        height: 4rem;
    }
}

@media screen and (max-width:560px) {
    *{
        font-size: 0.3rem;
    }

    .cart-item{
        height: 3rem;
    }
}
</style>