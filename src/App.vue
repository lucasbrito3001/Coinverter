<template>
    <header class="header-page">
      <HeaderContent/>
    </header>
  
    <div class="container">
  
      <main id="main-content">
        <section id="exchange-rate">
          <h2>Alteração 24h</h2>
          <ExchangeRate :arrayExchangeRateInfos="arrayExchangeRate"/>
          <p><strong>Obs:</strong> Passe para o lado para ver mais</p>
        </section>
        <section id="converter-interface">
          <ConverterInterface :currenciesSelectConverter="arraySelectConverter" :currenciesSelectConverterTarget="arraySelectConverterTarget" :ratiosConverter="arrayBidConverter" :ratiosTarget="arrayBidTarget"/>
        </section>
      </main>
      <aside id="aside-content">
        <section id="tablePage">
          <h2>Tabela de Valores Atualizada</h2>
          <table>
            <thead>
              <tr>
                <TableHead v-for="headData in arrayTableHead" :key="headData" :table-head="headData"/>
              </tr>
            </thead>
            <tbody>
              <TableBody v-for="bodyData in arrayTableData" :key="bodyData" :table-infos="bodyData"/>
            </tbody>
          </table>
        </section>
        <section class="row" id="aboutConverter">
          <AboutConverter/>
        </section>
        <section id="aboutBitcoin">
          <AboutBitcoin/>
        </section>
      </aside>
  
    </div>
  
    <footer class="footer-page">
      <div class="feedback">
        <h2>Esse site foi útil pra você? Entre em contato comigo por essas redes sociais, e me dê um feedback para buscar sempre melhorar a sua experiência!</h2>
      </div>
      <div>
        <strong>GitHub: </strong> <a href="https://github.com/lucasbrito3001" target="blank">https://github.com/lucasbrito3001</a>
      </div>
      <div>
        <strong>LinkedIn: </strong> <a href="https://linkedin.com/in/webdevbrito" target="blank">https://linkedin.com/in/webdevbrito</a>
      </div>
      <div>
        <strong>Twitter: </strong> <a href="https://twitter.com/brito3001" target="blank">https://twitter.com/brito3001</a>
      </div>
    </footer>
</template>

<script>
import HeaderContent from "./components/HeaderContent.vue"
import TableHead from "./components/TableHead.vue"
import TableBody from "./components/TableBody.vue"
import ConverterInterface from "./components/ConverterInterface.vue"
import ExchangeRate from "./components/ExchangeRate.vue"
import AboutConverter from "./components/AboutConverter.vue"
import AboutBitcoin from "./components/AboutBitcoin.vue"

export default {
  name: 'App',
  components: {
    HeaderContent,
    ExchangeRate,
    ConverterInterface,
    TableHead,
    TableBody,
    AboutConverter,
    AboutBitcoin
  },

  data(){
    return {
      responseAPI: '',
      currenciesAbbr: ["USD","BTC", "CAD","GBP","EUR","LTC","JPY","ILS","ARS","AUD","CHF","CNY","XRP"],
      arrayTableHead: ["Sigla", "Moeda", "Cotação", "Alteração 24h (%)"],
      arrayTableData: [],
      arraySelectConverter: [],
      arraySelectConverterTarget: [],
      arrayBidConverter: [],
      arrayBidTarget: [],
      arrayExchangeRate: [],
      fillSelects: true,
      codeConverted: -1,
      codeTarget: -1
    }
  },

  created(){
    this.requestAPI()
    this.updateAPI()
  },

  methods : {

    async requestAPI() {
      try {

        const response = await fetch('https://economia.awesomeapi.com.br/json/all')
        const data = await response.json()

        this.responseAPI = data

        this.selectTableDatas()

        if(this.fillSelects){
          this.selectConverterCurrencies()
          this.fillSelects = false
        }

        this.updateBid()

        this.updateExchangeRate()

      } catch (error) {
        console.error(error)
      }
    },

    selectTableDatas(){
      this.arrayTableData = []
      for(let index in this.currenciesAbbr){
        let currency = this.currenciesAbbr[index]
        
        this.arrayTableData.push({
          code: this.responseAPI[currency].code,
          name: this.responseAPI[currency].name,
          bid: (new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' }).format(this.responseAPI[currency].bid)),
          pctChange: Number(this.responseAPI[currency].pctChange).toFixed(2)
        })
      }
    },

    selectConverterCurrencies(){

      this.arraySelectConverterTarget.push({
        name: 'Real',
        code: ++this.codeTarget,
      })
      for(let index in this.currenciesAbbr){
        let currency = this.currenciesAbbr[index]
        
        this.arraySelectConverter.push({
          name: this.responseAPI[currency].name,
          code: ++this.codeConverted,
        })

        this.arraySelectConverterTarget.push({
          name: this.responseAPI[currency].name,
          code: ++this.codeTarget,
        })
      }
      this.arraySelectConverter.push({
        name: 'Real',
        code: ++this.codeConverted,
      })

    },

    updateBid(){

        this.arrayBidConverter = []
        this.arrayBidTarget = []

        this.arrayBidTarget.push(Number(1))

        for(let index in this.currenciesAbbr){
          let currency = this.currenciesAbbr[index]

          this.arrayBidConverter.push(Number(this.responseAPI[currency].bid).toFixed(2))

          this.arrayBidTarget.push(Number(this.responseAPI[currency].bid).toFixed(2))

        }

        this.arrayBidConverter.push(Number(1))

    },

    updateExchangeRate(){
      this.arrayExchangeRate = []

      for(let index in this.currenciesAbbr){
        let currency = this.currenciesAbbr[index]

        this.arrayExchangeRate.push({
          code: this.responseAPI[currency].code,
          pctChange: Number(this.responseAPI[currency].pctChange).toFixed(2)
        })
      }

    },

    updateAPI(){
      setInterval( () => {
        this.requestAPI()
      },30000)
    }

  }
  
}
</script>

<style>

:root {
  --nav-link: gray;
  --light-blue: rgb(158,158,255);
  --default-blue: rgb(24, 24, 158);
  --text-color: black;
  --body-color: white;
}

body {
  overflow-x: hidden;
}

html {
  scroll-behavior: smooth;
}

* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
  color: var(--text-color);
}

p {
  font-size: .9rem;
}

header {
  height: fit-content;
  border-bottom: 6px solid var(--default-blue);
  box-shadow: 1px 2px 3px var(--nav-link);
  z-index: 100;
  background-color: var(--body-color);
  position: fixed;
  top: 0px;
  width: 100%;
}

.container {
  display: grid;
  max-width: 1000px;
  margin: auto;
}

/* Main Style */

#main-content {
  max-width: 1000px;
  height: 88vh;
  margin: 14vh 0 0;
  overflow-x: hidden;
}

#exchange-rate {
  width: 100%;
}

#exchange-rate h2 {
  font-size: .9rem;
}

#exchange-rate p{
  font-size: .73rem;
}

/* Table Style */

table {
  margin: 0;
  position: relative;
  border-collapse: collapse;
  font-size: .85rem;
  width: 100%;
  text-align: center;
}

#tablePage {
  padding-top: 12vh;
}

#tablePage h2 {
  margin-bottom: 2vh;
  font-size: 1.2rem;
}

table thead {
  background: var(--default-blue);
}

table thead th{
  color: white;
  font-weight: normal;
  padding: 5px;
}

/* Footer */

footer {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  padding: 5vh 0;
  border-top: 5px solid var(--default-blue);
}

footer .feedback {
  width: 100%;
}

footer h2 {
  width: fit-content;
  padding: 5px 15px;
  text-align: center;
  margin: 0 auto 5vh;
  font-size: 1rem;
  color: var(--default-blue);
  font-weight: normal;
  box-shadow: 1px 2px 3px gray;
  border-radius: 10px;
}

/* ============================== */
@media(max-width:992px){
  table {
    font-size: .8rem;
  }
}

@media(max-width:768px){
  h2 {
    font-size: 1rem;
  }

  p {
    font-size: .83rem;
  }

  .container {
    margin: 0 10px;
  }
}

</style>
