<template>
    <!-- Shopping Items -->
    <div class="shopping-items">
        <!-- Shopping Item -->
        <div class="shopping-item">
           <div 
                v-for="item in searchItem" 
                :key="item.id" 
            >   
                <ShoppingItem 
                    :item="item" 
                    @addToCart="addToCart" 
                    :cartActive="cartActive" 
                />
           </div>
        </div>
        <!-- End Of Shopping Item -->
    </div>
    <!-- End Of Shopping Items -->
</template>

<script>
    import ShoppingItem from './ShoppingItem.vue';
    export default {
        components:{
            ShoppingItem
        },
        /* Props */
        props:['searchingText','removedIndex'],
        watch:{
            removedIndex(remIndex){
                this.cartActive = {
                    id:remIndex.id,
                    logic:false,
                };
            },
            searchingText(last){
                const search = new RegExp(last);

                this.searchItem = this.items.filter(item => {
                    for(let property of Object.keys(item)){
                        if(search.test(item[property])){
                            return true;
                            break;
                        }
                    }
                });
                
                if( last = '' ){
                    this.searchItem = this.items;
                }
            }
        },
        /* Data */
        data() {
            return {
                items:[
                    {
                        id:0,
                        model:"vivo v15",
                        RAM:"6 GB",
                        internalMemory:"64 GB",
                        rearCamera:"12 MP",
                        frontCamera:"30 MP",
                        screenSize:"16.51 cm",
                        avatar:"https://www.91-img.com/pictures/132721-v10-vivo-v15-pro-mobile-phone-large-1.jpg?tr=h-330,c-at_max,q-60",
                        price:"156"
                    },
                    {
                        id:1,
                        model:"redmi a3",
                        RAM:"4 GB",
                        internalMemory:"64 GB",
                        rearCamera:"48 MP",
                        frontCamera:"30 MP",
                        screenSize:"17.27 cm",
                        avatar:"https://img2.ibay.com.mv/is1/full/2019/08/item_2710902_574.jpg",
                        price:"111"
                    
                    },
                    {
                        id:2,
                        model:"redmi note 7 pro",
                        RAM:"4 GB",
                        internalMemory:"64 GB",
                        rearCamera:"5 MP",
                        frontCamera:"13 MP",
                        screenSize:"16 cm",
                        avatar:"https://www.giztop.com/media/catalog/product/cache/dc206057cdd42d7e34b9d36e347785ca/x/i/xiaomi_redmi_note_7_pro.jpg",
                        price:"129"
                    },
                    {
                        id:3,
                        model:"redmi 9A",
                        RAM:"2 GB",
                        internalMemory:"32 GB",
                        rearCamera:"13 MP",
                        frontCamera:"5 MP",
                        screenSize:"16.51 cm",
                        avatar:"https://gloimg.gbtcdn.com/storage/item/6615272824267153408/15946/27289d2d1998.jpg",
                        price:"77.49"
                    },
                    {
                        id:4,
                        model:"redmi note 7 pro",
                        RAM:"4 GB",
                        internalMemory:"64 GB",
                        rearCamera:"5 MP",
                        frontCamera:"13 MP",
                        screenSize:"16 cm",
                        avatar:"https://www.giztop.com/media/catalog/product/cache/dc206057cdd42d7e34b9d36e347785ca/x/i/xiaomi_redmi_note_7_pro.jpg",
                        price:"129"
                    },
                    {
                        id:5,
                        model:"Apple iPhone 11 ",
                        RAM:"Compatible Phone Model:Apple",
                        internalMemory:"64 GB",
                        rearCamera:"Air cushion technology",
                        frontCamera:" Durable ",
                        screenSize:"Perfect fit",
                        avatar:"https://coolstuf.com.pg/wp-content/uploads/2020/05/iPhone-11-1-1.jpg",
                        price:"1244"
                    },
                    {
                        id:6,
                        model:"Samsung Galaxy",
                        RAM:"6 GB",
                        internalMemory:"128 GB",
                        rearCamera:"5 MP",
                        frontCamera:"32 MP",
                        screenSize:"16.25 cm",
                        avatar:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR283p4rNHLgM5x5pdvBaD2sB9sNgzc3brTVg&usqp=CAU",
                        price:"179.9"
                    },
                    {
                        id:7,
                        model:"iPhone 7",
                        RAM:"Compatible Phone Model:iPhone 7",
                        internalMemory:"Durable",
                        rearCamera:"Phone logo display",
                        frontCamera:"Light weight",
                        screenSize:"Perfect fit",
                        avatar:"https://www.gizmochina.com/wp-content/uploads/2016/09/iphone7-plus-5-1-500x500.jpg",
                        price:"2490"
                    }
                ],
                searchItem:null,
                cartActive:null
            }
        },
        /* Created */
        created() {
            this.searchItem = this.items;
        },
        /* Methods */
        methods: {
            addToCart(id){
                const selectedItem = this.items.find( item => item.id == id );
                
                if(selectedItem){
                    this.$emit('selectedItem',selectedItem);
                }
            }
        },
    }
</script>

<style lang="scss" scoped>
.shopping-items{
    margin:2rem;
    background: #f1f1f1;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    

    .shopping-item{
        display: grid;
        grid-template-columns: repeat(2,1fr);

        @media screen and (max-width:1100px){                                       
            &{
                grid-template-columns: repeat(1,1fr);
            }
        }
    }

    @media screen and (max-width:1100px){
        &{
            margin:1rem;
        }        
    }

}
</style>