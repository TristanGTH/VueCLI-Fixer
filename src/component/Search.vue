<template>
        <ion-item>
            <ion-input type="number" id="searchbar" placeholder="Mettez une valeur en euros et choisissez la monnaie de conversion" ></ion-input>
            <ion-select placeholder="$" ok-text="Confirmer" cancel-text="Retour" id="select">
                <ion-select-option v-for="(item,name) in currency" :key="name" :value="item">{{name}}</ion-select-option>
            </ion-select>
        </ion-item>

        <ion-button @click="showValue">Convertir</ion-button>
</template>

<script>
    import {defineComponent} from 'vue';
    import axios from 'axios'
    import {  IonItem, IonInput, IonButton, IonSelect, IonSelectOption } from '@ionic/vue';

    export default defineComponent({
        name: "Search",
        data(){
            return{
                currency: null,
            }
        },
        components:{
            IonButton,
            IonInput,
            IonItem,
            IonSelect,
            IonSelectOption
        },
        methods:{
            async showValue(){
                let money = document.getElementById('select').value
                let searchbar = document.getElementById('searchbar').value
                let transformed = searchbar * money
                this.bus.emit('finalCurrency', transformed)
            }
        },
        mounted() {
            axios.get('http://data.fixer.io/api/latest?access_key='+process.env.VUE_APP_API_KEY)
                .then((response) =>{
                    this.currency = response.data.rates
                })
                .catch(function (error) {
                    console.log(error)
                })
        }
    });


</script>

<style scoped>

    .test{
        background-color: white;
    }
</style>