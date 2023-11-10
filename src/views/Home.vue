<template>
    <ion-page>
        <ion-header>
        </ion-header>
        <ion-content>
            <ion-card>
            <ion-card-content>
                <!-- dibawah ini adalah komponen ion-row dan ion-button yang akan kita gunakan untuk mengambil data dari API -->
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
                
                <!-- dibawah ini adalah komponen ion-item yang akan kita gunakan untuk menampilkan data dari API -->
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
        name: 'Home', // nama komponen yang akan kita gunakan
        data() {
            return {
                cryptoData: [], // variabel untuk menampung data dari API
            };
        },
        
        methods: {
            async fetchCryptocurrencyData() {
                try {
                    const response = await axios.get('https://api.coinlore.net/api/tickers/'); // API yang digunakan untuk mengambil data cryptocurrency
                    this.cryptoData = response.data.data; // data yang diambil disimpan ke dalam variabel cryptoData
                
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
