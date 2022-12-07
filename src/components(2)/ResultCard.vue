<template>
    <div class="container">
        <h2>Your totem animal is:</h2>
        <h1 style="color: rgb(21 143 19);">{{animal.name.toUpperCase()}}</h1>

        <img :src="animal.img" alt="" style="width: 600px;"/>

        <div class="disc">
            {{animal.desc}}
        </div>
    </div>
</template>

<script>
export default {
    props: ['animal']
}
</script>

<style scoped>
    .disc{
        padding: 20px;
    }

    .container {
        background: #fff;
        width: 800px;
    }

    h2 {
        position: relative;
        top: 15px;
    }
</style>