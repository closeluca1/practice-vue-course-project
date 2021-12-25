<template>
    <div class="message-container">
        <p>{{ msg }}</p>
    </div>
</template>

<script>
export default {
    name: "Mesage",
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container{
        max-width: 400px;
        padding: 10px;
        margin: 30px auto;
        border-radius: 4px;
        border: 2px solid #b8daff;
        color: #004085;
        background: #cce5ff;
    }
</style>