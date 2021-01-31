<template>
    <ion-content>{{finalResult}}</ion-content>
</template>

<script>
    import {defineComponent} from 'vue';

    export default defineComponent({
        data(){
            return{
                finalResult: ''
            }
        },
        name: "Results",

        mounted() {
           this.bus.on('finalCurrency', (transformed) =>{ this.finalResult = transformed})
        }
    })
</script>

<style scoped>

</style>