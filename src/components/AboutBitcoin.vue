<template>
    <div class="row">
        <h2 class="col-12">Sobre BitCoin</h2>
        <div class="flex-row">
            <div class="bitcoin-div-img">
                <img class="bitcoin-images" src="../assets/increase.svg" alt="bitcoin-increase">
            </div>
            <div class="bitcoin-div-text">
                <h3>
                    Afinal, o que é Bitcoin?
                </h3>
                <p>
                    O Bitcoin surgiu em 2009, com o intuito de ser uma moeda virtual que facilitaria negociações P2P (Peer to Peer) pela internet, ou seja negociações de pessoa para pessoa de forma mais rápida, com taxas menores, alto nível de segurança, e que pudesse ser realizada e utilizada em qualquer lugar do mundo. Isso é possível pelo fato da moeda ser descentralizada, o que significa que não tem nenhum banco, ou qualquer instituição financeira por trás dessas transações.
                </p>
                <p>
                    No seu início, 1 Bitcoin não tinha valor algum, porém com a adesão do projeto pela comunidade, a moeda teve uma valorização radical, e hoje em dia por exemplo está valendo incríveis <span style="color: var(--result)">R$ {{bitcoinBid}}</span> !!
                </p>
            </div>
        </div>
        <div class="flex-row">
            <div class="bitcoin-div-img">
                <img class="bitcoin-images" src="../assets/asic.svg" alt="mining-bitcoin">
            </div>
            <div class="bitcoin-div-text">
                <h3>
                    A mineração do Bitcoin
                </h3>
                <p>
                    Quando falamos de mineração de Bitcoin, temos que entrar no conceito de blockchain, então vamos lá, o que é blockchain?
                </p>
                <p>
                    A blockchain, ou cadeia de blocos, resumidamente é uma rede de negócios onde todas as suas transações são gravadas no ledger, ou livro-razão, sendo que, se forem uma vez gravadas não podem mais ser apagadas, e todo participante tem uma cópia desse livro onde seu conteúdo é constantemente sincronizado entre elas. E então é nela que ficam armazenados os resultados das minerações de Bitcoin.
                </p>
                <p>
                    A mineração de bitcoin pode ser descrita de maneira resumida como a validação do código de uma negociação de bitcoins, mas ela se baseia em descobrir se o código de um bloco escrito é válido por meio de cálculos matemáticos muito complexos, sendo esse código chamado de <em><strong>hash</strong></em> ou assinatura digital, esse hash é gerado pela "compactação" de informações inseridas no bloco, e é passado para um novo sempre que um outro é quebrado. Então a função dos mineradores é oferecer poder computacional, no caso do bitcoin, poder de processamento providos de placas de vídeo potentes, para realizar os cálculos e verificar esses códigos para então validá-los, e quando isso acontece, o bloco é quebrado e a recompensa em bitcoin é dividida pelos mineradores que participaram dessa quebra.
                </p>
            </div>
        </div>
        
        <div class="flex-row">
            <div class="bitcoin-div-img">
                <img class="bitcoin-images" src="../assets/ico.svg" alt="bitcoin-increase">
            </div>
            <div class="bitcoin-div-text">
                <h3>
                    Como funciona a Divisão da Recompensa
                </h3>
                <p>
                    Essa divisão é baseada na Prova de Trabalho que é o significado da sigla PoW (Proof of Work) de cada minerador. Então sua recompensa será de acordo com o poder de processamento que você forneceu para a rede de mineradores realizar a quebra do bloco. Hoje existem as chamadas Farms de Bitcoin, que é basicamente um local enorme cheio de placas de vídeo funcionando a todo momento fornecendo um enorme poder de processamento para um ou vários grupos de mineração, isso é viável exatamente por conta do conceito de PoW.
                </p>
            </div>
        </div>
        <div class="flex-row">
            <div class="bitcoin-div-img">
                <img src="../assets/transaction.svg" alt="transaction-bitcoin" class="bitcoin-images">
            </div>
            <div class="bitcoin-div-text">
                <h3>
                    E pra onde vão esses Bitcoins?
                </h3>
                <p>
                    Pra sua carteira de bitcoin, que é uma carteira digital onde as senhas privadas e públicas das suas moedas são guardadas, ou seja, o código gerado na transação do saldo de uma carteira para outra, que foi armazenado na blockchain, é um tipo de comprovante do seu saldo em bitcoin, então é muito importante guardar todas essas informações, para que futuramente você não perca suas moedas, cada carteira tem uma identificação, podendo ser em forma de números e letras, ou uma sequência de palavras em inglês que devem ser guardados de maneira ordenada. Essa carteira pode ser guardada online em computadores e aplicativos de celulares, ou offline, em dispositivos sem conexão com a internet, pen-drives, ou simplesmente escritos em um papel, os métodos offline são de certa forma mais seguros, porque assim ninguém consegue te hackear e acessar essas informações.
                </p>
                <p>
                    Exisem também as Exchanges que são empresas que trabalham diretamente com essas negociações de compra, venda e transferência entre carteiras virtuais de bitcoin, esse tipo de carteira tem uma desvantagem que se o sistema delas cair, você não tem acesso a sua carteira, e se precisasse fazer uma negociação naquele exato momento, lascou... Porém é uma maneira simples para quem quer comprar e investir em bitcoin sem precisar saber como funciona a fundo essas negociações, e também procuram ter um investimento bastante seguro. Segue o link de algumas exchanges bastante conhecidas: <br>
                    
                </p>
                <ul id="exchanges">
                        <li><a href="https://www.mercadobitcoin.com.br/" target="blank">Mercado Bitcoin</a></li>
                        <li><a href="https://www.binance.com/pt-BR/" target="blank">Binance</a></li>
                        <li><a href="https://foxbit.com.br/" target="blank">FoxBit</a></li>
                    </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            bitcoinBid: ''
        }
    },

    created(){
        this.bitcoinBidUpdate()
        setInterval( () => {
            this.bitcoinBidUpdate()
        },30000)
    },

    methods: {
        async bitcoinBidUpdate(){
            const response = await fetch(`https://economia.awesomeapi.com.br/all/BTC-BRL`)
            const data = await response.json()
            this.bitcoinBid = data['BTC'].bid
        }
    }
}
</script>

<style scoped>

.flex-row {
    display: flex;
    align-items: center;
}

.row{
    padding-top: 12vh;
}
.row h2{
    font-size: 1.5rem;
    font-weight: bold;
    border-bottom: 2px solid var(--default-blue);
    margin-bottom: 7vh;
}

.row h3{
    font-size: 1.2rem;
    font-weight: bold;
}

.row p{
    text-align: justify;
    margin-top: 2vh;
    line-height: 1.5;
}

div{
    margin-bottom: 7vh;
}

.bitcoin-div-img {
    width: 30%;
}

.bitcoin-images{
    width: 45%;
}

.bitcoin-div-text {
    width: 70%;
}


.bitcoin-div-text h3 {
    border-bottom: 2px solid var(--default-blue);
    margin-bottom: 2vh;
}

#exchanges{
    list-style: none;
    margin-top: 20px;
    display: flex;
    justify-content: space-evenly;
}

#exchanges li{
    font-size: 1.2rem;
    border: 1px solid var(--default-blue);
    border-radius: 5px;
    padding: 2px;
    background-color: var(--default-blue);
}

#exchanges a{
    color: white;
    text-decoration: none;
}

@media(max-width: 992px){
    .flex-row {
        flex-direction: column;
    }
    .bitcoin-div-img {
        width: 15%;
    }

    .bitcoin-images{
        width: 100%;
        margin: auto;
    }

    .bitcoin-div-text {
        width: 90%;
        margin: auto;
    }
}

@media(max-width:768px){
    .bitcoin-div-img {
        width: 25%;
    }
    .row h2{
        font-size: 1.1rem;
    }

    .row h3{
        font-size: .95rem;
    }
}
</style>