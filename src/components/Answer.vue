<template>
    <div class="alert alert-success" role="alert">
        <h1>That's correct!</h1>
        <hr>
        <button class="btn btn-primary" @click="onNextQuestion">Next Question</button>
    </div>
</template>

<script>
    export default {
        name: "answer",
        methods:{
            onNextQuestion(){
                this.$emit('confirmed')
            }
        }
    }
</script>

<style scoped>

</style>