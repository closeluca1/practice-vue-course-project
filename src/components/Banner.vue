<template>
    <div id="main-banner">
        <h1>Monte seu Hamburger</h1>    
    </div>    
</template>

<script>
    export default {
        
    }
</script>

<style scoped>  
    #main-banner{
        min-height: 50vw;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        background-position: 0 60vw;
        background-size: cover;
        background-image: url('/img/burger.jpg')
    }
    #main-banner h1{
        padding: 20px 40px;
        text-align: center;
        font-size: 3vw;
        color: #fafafa;
        background: #222;
    }
</style>