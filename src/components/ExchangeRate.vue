<template>
    <ul class="listExchangeRate">
        <li v-for="singleCurrency in arrayExchangeRateInfos" :key="singleCurrency.code">{{singleCurrency.code}} : <span :id="singleCurrency.code">{{singleCurrency.pctChange}}% </span></li>
    </ul>
</template>

<script>
export default {
    props: ['arrayExchangeRateInfos'],

    mounted(){
        setTimeout( () => {
            this.statusDelta()
        },1000)
    },

    methods: {
        statusDelta(){
            for(let index in this.arrayExchangeRateInfos){
                let deltaSpan = document.querySelector(`#${this.arrayExchangeRateInfos[index].code}`)

                let delta = this.arrayExchangeRateInfos[index].pctChange

                if(delta <= 0){
                    deltaSpan.style.background = 'red'
                } else {
                    deltaSpan.style.background = 'rgb(0,175,0)'
                }
            }
        }
    }
}
</script>

<style scoped>

.listExchangeRate {
    position: relative;
    display: flex;
    overflow-x: scroll;
    height: 8vh;
    align-items: center;
}

.listExchangeRate li {
    display: inline-block;
    font-size: .75rem;
    min-width: 100px;
    height: 4vh;
    text-align: center;
    margin: 0 5px;
}

.listExchangeRate span {
    color: white;
    padding: 1px 4px;
    border-radius: 6.5px;
}

</style>