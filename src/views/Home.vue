<template>
    <ion-page>
        <ion-header>
        </ion-header>
        <ion-content>
            <ion-card>
            <ion-card-content>
                <ion-row class="ion-justify-content-center ion-align-items-center">
                    <ion-button @click="fetchCryptocurrencyData" expand="medium">Get Data</ion-button>
                </ion-row>
            </ion-card-content>
            </ion-card>
    
            <ion-card v-if="cryptoData.length > 0">
            <ion-card-content>
                <ion-list>
                <ion-item>
                    <ion-label>Name</ion-label>
                    <ion-label>Symbol</ion-label>
                    <ion-label>Harga USD</ion-label>
                </ion-item>
                <ion-item v-for="crypto in cryptoData" :key="crypto.id">
                    <ion-label>{{ crypto.name }}</ion-label>
                    <ion-label>{{ crypto.symbol }}</ion-label>
                    <ion-label>{{ crypto.price_usd }}</ion-label>
                </ion-item>
                </ion-list>
            </ion-card-content>
            </ion-card>
        </ion-content>
    </ion-page>
</template>

<script>
    import { defineComponent } from 'vue';
    import axios from 'axios';
    
    export default defineComponent({
        name: 'Home',
        data() {
            return {
                cryptoData: [],
            };
        },
        
        methods: {
            async fetchCryptocurrencyData() {
                try {
                    const response = await axios.get('https://api.coinlore.net/api/tickers/');
                    this.cryptoData = response.data.data;
                } catch (error) {
                    console.error('Error fetching cryptocurrency data:', error);
                }
            },
        },
    });
</script>

<style scoped>
    /* Add your CSS styles here */
</style>
