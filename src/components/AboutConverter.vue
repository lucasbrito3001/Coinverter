<template>
    <div class="col-12">
        <h2>Sobre o conversor</h2>
        <!-- <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Inventore placeat consectetur vel eligendi sint vitae numquam et quaerat doloremque, quia sunt amet doloribus odit exercitationem, praesentium illo, temporibus sit corporis. Lorem ipsum dolor sit, amet consectetur adipisicing elit. Error cupiditate recusandae ducimus veniam quam facilis dolores, hic labore ex aliquid? Tempora debitis veniam minima quisquam ipsa, nostrum repudiandae quis dignissimos? Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempore cum maxime veniam nemo quo! Voluptatem, quo, dignissimos dolore quas aperiam consequuntur aliquam, quasi et quaerat culpa ea corrupti nisi modi. Lorem ipsum dolor sit, amet consectetur adipisicing elit. Sit labore nulla quae obcaecati nobis hic possimus, minima doloribus dolorum adipisci voluptas recusandae id vel nostrum mollitia commodi, reprehenderit iure amet? Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi consequuntur architecto eum nihil officiis expedita, ullam dignissimos tempora dolores minima animi deleniti, sapiente eveniet rerum aliquid, magni porro debitis. Obcaecati? Lorem ipsum, dolor sit amet consectetur adipisicing elit. Atque at sunt minima possimus dolorum quia non eum quisquam consectetur repellat a eveniet esse expedita ut repellendus sed ipsum, totam sapiente!</p> -->
        <p>
            O foco do Coinverter é ser um conversor de moedas simples e prático, onde você consegue calcular os valores das moedas em relação as outras, e ficar por dentro das alterações dos mesmos a todo momento, porém, além disso, aqui você pode encontrar também, tabelas com informações interessantes das moedas, e ficar por dentro das notícias do mundo da economia com o blog de notícias, que é atualizado sempre que surge algum novo acontecimento interessante, e até mesmo entender mais sobre o que é o BitCoin, como comprar, técnicas de venda e compra, lucro, e etc... <br>
            Caso tenha alguma crítica construtiva, e se sinta confortável para enviar feedbacks sobre a plataforma, envie um e-mail para mim pelo link abaixo: <br> 
            <a href="mailto:devlucasmail@gmail.com?
            Subject=Feedback%20Coinverter" id="mail"><img src="../assets/gmail.svg" alt="logo-gmail" id="gmail"> Enviar e-mail!</a>
        </p>
    </div>    
</template>

<style scoped>
    .col-12{
        padding-top: 12vh;
    }
    .col-12 h2{
        font-size: 1.5rem;
        font-weight: bold;
        border-bottom: 2px solid var(--default-blue);
    }
    .col-12 p{
        text-align: justify;
        line-height: 1.5;
        margin: 2vh auto;
    }

    #mail{
        margin-top: 1.5rem;
        display: flex;
        align-items: center;
        font-size: 1.5rem;
        width: fit-content;
        padding: 0 .5rem;
        box-sizing: border-box;
        border-radius: 5px;
    }

    #gmail{
        width: 2.5rem;
        margin-right: 1rem;
    }

    @media(max-width: 768px){
        .col-12 p{
            width: 90%;
            margin: 2vh auto;
        }

        .col-12 h2 {
            font-size: 1.1rem;
        }
    }
</style>