<template>
    <div align="center">

        <h1 class="title">{{ num }} {{ nome }}</h1>
        <small class="subtitle">{{ url }}</small>
        <hr>

    </div>
</template>

<script>
export default {
    name: "Pokemon",
    props: {
        nome: String,
        url: String,
        num: Number
    }
}
</script>

<style>

</style>