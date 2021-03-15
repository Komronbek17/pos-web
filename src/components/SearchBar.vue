<template>
    <!-- Search Bar -->
    <div class="search-bar">
        <input type="text" v-model="searchText.msg" />
        <i class="fas fa-search"></i>
    </div>
</template>

<script>
    import { ref, watch, watchEffect } from 'vue'
    export default {
        setup(props,context) {
            let searchText=ref({msg:''});

            watchEffect(()=>{
                context.emit('searchFunc',searchText.value.msg);
            })

            return {
                searchText
            }
        }
    }
</script>

<style lang="scss" scoped>
/* Search Bar */
.search-bar{
    text-align: left;
    padding:0.1rem;
    position: relative;
    width:50vw;
    padding:0.3rem;
    border: none;
    outline: none;
    background: #E8EAE3;
    box-shadow: 0 0 5px rgba( #000000, 0.3);
    border: 1px solid #2A3166;
    border-top:1px solid #EE7879;
    border-bottom-right-radius: 15px ;
    border-top-left-radius: 15px ;
    transition: all 0.1s;
}

input{
    border:none;
    background: transparent;
    outline: none;
    font-family: 'Roboto', sans-serif;
    font-weight: 500;
    font-size: 1.2rem;
    width:90%;
    position: relative;
}

</style>