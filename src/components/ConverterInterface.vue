<template>
    <div class="row">

        <div class="card">
            <select name="convertedCurrency" id="convertedCurrency" class="converterSelects" @change="selectConvertedValue">
                <option v-for="selectCurrency in currenciesSelectConverter" :id="selectCurrency.code" :key="selectCurrency" :value="selectCurrency.code">{{selectCurrency.name}}</option>
            </select>
            <p><input type="number" id="convertedValue" class="converterSelects" v-model="inputConvertedCurrency" @input="calculateConversion"></p>
        </div>
        <div>
            <p class="converterSelects" id="equal" style="color: var(--default-blue)">equivale</p>
        </div>
        <div class="card">
            <select name="convertedCurrency" id="targetCurrency" class="converterSelects" @change="selectTargetValue">
                <option v-for="selectCurrency in currenciesSelectConverterTarget" :key="selectCurrency" :id="selectCurrency.code" :value="selectCurrency.code">{{selectCurrency.name}}</option>
            </select>
            <p class="converterSelects" id="res">{{outputTargetCurrency}}</p>
        </div>

    </div>
</template>

<script>
export default {
    props: ['currenciesSelectConverter', 'currenciesSelectConverterTarget', 'ratiosConverter', 'ratiosTarget'],

    data(){
        return{
            ratio: 0,
            valueConvertedCurrency: 0,
            valueTargetCurrency: 0,
            inputConvertedCurrency: (Number(1.00).toFixed(2)),
            outputTargetCurrency: 0,
            verifyOptions: false
        }
    },

    mounted(){
        setTimeout( () => {
            this.bidRatio();
        }, 1000)
    },

    methods: {
        selectConvertedValue(){
            const selectConvertedCurrency = document.querySelector('#convertedCurrency')
            this.valueConvertedCurrency = selectConvertedCurrency.value
            this.bidRatio()
        },

        selectTargetValue(){
            const selectTargetCurrency = document.querySelector('#targetCurrency')
            this.valueTargetCurrency = selectTargetCurrency.value
            this.bidRatio()
        },

        bidRatio(){
            
            const bidConverted = this.ratiosConverter[this.valueConvertedCurrency]
            const bidTarget = this.ratiosTarget[this.valueTargetCurrency]

            this.ratio = Number(bidConverted) / Number(bidTarget)

            this.calculateConversion()

        },

        calculateConversion(){
            if(this.valueTargetCurrency == 2){
                this.outputTargetCurrency = (Number(this.inputConvertedCurrency) * Number(this.ratio)).toLocaleString('pt-BR', {minimumFractionDigits : 10, maximumFractionDigits : 10})
            } else {
                this.outputTargetCurrency = (Number(this.inputConvertedCurrency) * Number(this.ratio)).toLocaleString('pt-BR', {minimumFractionDigits : 2, maximumFractionDigits : 2})
            }
        }
    }
}
</script>

<style scoped>
    .row{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-around;
        margin-top: 15vh;
    }

    .card {
        width: 45%;
        border-radius: 10px;
        box-shadow: .5px .5px 3px gray
    }

    .converterSelects {
        width: 100%;
        height: 6.5vh;
    }

    select {
        border: none;
        border-radius: 10px 10px 0 0;
        border-bottom: 1px solid #ddd;
        padding-left: 10px;
    }

    select:focus {
        outline: none;
    }

    option {
        background-color: white;
        font-size: .9rem;
    }

    input {
        border: none;
        outline: none;
        text-align: center;
        border-radius: 0 0 10px 10px;
        font-size: 2rem;
    }
    
    #res {
        border-radius: 0 0 10px 10px;
        text-align: center;
        line-height: 6.5vh;
        overflow-y: hidden;
        font-size: 2rem;
        color: var(--default-blue);
    }

    #equal {
        line-height: 10vh;
        height: 10vh;
    }

    @media(max-width: 992px){
        input {
            font-size: 1.5rem;
        }

        #res { 
            font-size: 1.5rem;
        }

        option {
            background-color: white;
            font-size: .8rem;
            padding: 0px;
        }
    }

    @media(max-width: 768px){

        .row {
            flex-direction: column;
        }

        .card {
            width: 90%;
        }
    }

</style>