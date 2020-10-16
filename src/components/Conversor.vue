<template>
    <div class="conversor">
        <h2>{{moedaA}} to {{moedaB}}</h2>
        <input type="text" v-model="moedaA_value" v-bind:placeholder = "moedaA">
        <input type="button" value="Conversor" v-on:click="converter">
        <h2>{{moedaB_value}}</h2>
        
    </div>
</template>

<script>
export default {
    name: "Conversor",
    props: ["moedaA", "moedaB"],
    data() {
        return {
            moedaA_value: "",
            moedaB_value: 0
        }
    },
    methods:{
        converter(){
            let de_para = this.moedaA + "_" + this.moedaB
            let url = "https://free.currencyconverterapi.com/api/v7/convert?q="+de_para+"&compact=ultra&apiKey=121f4cf466255a8a9764"
            fetch(url)
            .then(res=> {
                return res.json();
                })
                 .then(json=> {
                            let cotaçao = json[de_para]
                            this.moedaB_value = (cotaçao * parseFloat(this.moedaA_value)).toFixed(2)
                        })
            
        }
    }
}
</script>

<style scoped>

.conversor{

    max-width: 300px;
    padding: 30px;
    box-shadow: 0px 4px 8px;
}
    
</style>
    
