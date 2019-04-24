<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <h1>{{ msgff }}</h1>
        <button v-on:click="onClickMe">open Mouse</button>
    </div>
</template>


<script>
export default {
    data: function (){
        return {
            msg: 'hello from components a!'
        }
    },
    props:['msgff'],
    methods: {
        onClickMe: function (){
           //console.log(this.msgff)
           //this.$emit('child-tell-something',this.msg);
           this.$emit('child-tell-something',this.msg);
        }
    }
}
</script>


<style scoped>
h1 {
    color: #42b983
}
</style>
