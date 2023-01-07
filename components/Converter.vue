<template>
    <section>
        <div class="container">
            <h1>Value Converter</h1>
            <div class="upperContainer">
                <select name="first-currency" id="first-currency" v-model="currency_one">
                    <option value="AED">AED</option>
                    <option value="ARS">ARS</option>
                    <option value="AUD">AUD</option>
                    <option value="BGN">BGN</option>
                    <option value="BRL">BRL</option>
                    <option value="BSD">BSD</option>
                    <option value="CAD">CAD</option>
                    <option value="CHF">CHF</option>
                    <option value="CLP">CLP</option>
                    <option value="CNY">CNY</option>
                    <option value="COP">COP</option>
                    <option value="CZK">CZK</option>
                    <option value="DKK">DKK</option>
                    <option value="DOP">DOP</option>
                    <option value="EGP">EGP</option>
                    <option value="EUR">EUR</option>
                    <option value="FJD">FJD</option>
                    <option value="GBP">GBP</option>
                    <option value="GTQ">GTQ</option>
                    <option value="HKD">HKD</option>
                    <option value="HRK">HRK</option>
                    <option value="HUF">HUF</option>
                    <option value="IDR">IDR</option>
                    <option value="ILS">ILS</option>
                    <option value="INR">INR</option>
                    <option value="ISK">ISK</option>
                    <option value="JPY">JPY</option>
                    <option value="KRW">KRW</option>
                    <option value="KZT">KZT</option>
                    <option value="MXN">MXN</option>
                    <option value="MYR">MYR</option>
                    <option value="NOK">NOK</option>
                    <option value="NZD">NZD</option>
                    <option value="PAB">PAB</option>
                    <option value="PEN">PEN</option>
                    <option value="PHP">PHP</option>
                    <option value="PKR">PKR</option>
                    <option value="PLN">PLN</option>
                    <option value="PYG">PYG</option>
                    <option value="RON">RON</option>
                    <option value="RUB">RUB</option>
                    <option value="SAR">SAR</option>
                    <option value="SEK">SEK</option>
                    <option value="SGD">SGD</option>
                    <option value="THB">THB</option>
                    <option value="TRY">TRY</option>
                    <option value="TWD">TWD</option>
                    <option value="UAH">UAH</option>
                    <option value="USD">USD</option>
                    <option value="UYU">UYU</option>
                    <option value="VND">VND</option>
                    <option value="ZAR">ZAR</option>
                </select>
                <input type="number" name="input-one" id="input-one" v-model="amountOne" @input="fetchData()">
            </div>
            <div class="midContainer">
                <button>Switch</button>
            </div>
            <div class="bottomContainer">
                <select name="second-currency" id="second-currency" v-model="currency_two">
                    <option value="AED">AED</option>
                    <option value="ARS">ARS</option>
                    <option value="AUD">AUD</option>
                    <option value="BGN">BGN</option>
                    <option value="BRL">BRL</option>
                    <option value="BSD">BSD</option>
                    <option value="CAD">CAD</option>
                    <option value="CHF">CHF</option>
                    <option value="CLP">CLP</option>
                    <option value="CNY">CNY</option>
                    <option value="COP">COP</option>
                    <option value="CZK">CZK</option>
                    <option value="DKK">DKK</option>
                    <option value="DOP">DOP</option>
                    <option value="EGP">EGP</option>
                    <option value="EUR">EUR</option>
                    <option value="FJD">FJD</option>
                    <option value="GBP">GBP</option>
                    <option value="GTQ">GTQ</option>
                    <option value="HKD">HKD</option>
                    <option value="HRK">HRK</option>
                    <option value="HUF">HUF</option>
                    <option value="IDR">IDR</option>
                    <option value="ILS">ILS</option>
                    <option value="INR">INR</option>
                    <option value="ISK">ISK</option>
                    <option value="JPY">JPY</option>
                    <option value="KRW">KRW</option>
                    <option value="KZT">KZT</option>
                    <option value="MXN">MXN</option>
                    <option value="MYR">MYR</option>
                    <option value="NOK">NOK</option>
                    <option value="NZD">NZD</option>
                    <option value="PAB">PAB</option>
                    <option value="PEN">PEN</option>
                    <option value="PHP">PHP</option>
                    <option value="PKR">PKR</option>
                    <option value="PLN">PLN</option>
                    <option value="PYG">PYG</option>
                    <option value="RON">RON</option>
                    <option value="RUB">RUB</option>
                    <option value="SAR">SAR</option>
                    <option value="SEK">SEK</option>
                    <option value="SGD">SGD</option>
                    <option value="THB">THB</option>
                    <option value="TRY">TRY</option>
                    <option value="TWD">TWD</option>
                    <option value="UAH">UAH</option>
                    <option value="USD">USD</option>
                    <option value="UYU">UYU</option>
                    <option value="VND">VND</option>
                    <option value="ZAR">ZAR</option>
                </select>
                <input type="number" name="input-two" id="input-two" v-model="amountTwo"  @input="fetchData2()">
            </div>
        </div>
    </section>
</template>

<script lang="ts">
import { anyTypeAnnotation } from '@babel/types';
import Vue from 'vue';

export default Vue.extend({
    data(){
        return{
            data: [],
            currency_one: "USD",
            currency_two: "EUR",
            rate: 2,
            amountOne: 1,
            amountTwo: 2,
        };
    },

    methods: {
        fetchData(){
            fetch(`https://v6.exchangerate-api.com/v6/c6a8a8485acfa89c04d8ee8c/latest/${this.currency_one}`
            )
            .then((res) => res.json())
            .then((data) => {
                console.log(data);
                this.data = data;
                this.rate = data.conversion_rates[this.currency_one];
            })
            this.amountTwo = this.amountOne * this.rate;
        },

        fetchData2(){
            this.amountOne = this.amountTwo * this.rate;
        }

    },

    mounted(){
        this.fetchData();
        // this.fetchData2();
    }
})
</script>

<style scoped>

section{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh
}
.container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: auto;
    width: 500px;
    border: 1px solid black;
    border-radius: 8px;
    background: #e5e5e5;
    padding: 8px;
}

.container h1{
    font-family:Georgia, 'Times New Roman', Times, serif;
    font-size: 42px;
}
.upperContainer, .bottomContainer{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-around;
    margin-top: 18px;
}
.midContainer{
    margin-top: 16px;
}
.midContainer button{
    padding: 8px 18px;
    font-size: 16px;
    font-family:Verdana, Geneva, Tahoma, sans-serif;
    font-weight: 500;
    border-radius: 8px;
    border: 1px solid #090909;
    cursor: pointer;
}

select{
    padding: 8px 18px;
    font-family:Verdana, Geneva, Tahoma, sans-serif;
    margin: 8px;
}

input{
    margin: 8px;
    padding: 8px;
    font-size: 16px;
    font-family:Georgia, 'Times New Roman', Times, serif;
}
</style>