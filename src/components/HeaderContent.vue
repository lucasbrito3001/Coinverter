<template>
    <nav>
        <div class="responsive-menu">
            <a href="index.html" class="navbar-brand"><img src="../assets/brand.svg" alt="coinverter-brand"> Coinverter</a>
            <button type="button" class="navbar-toggler" @click="showMenu">
                <span class="sandwich"></span>
                <span class="sandwich"></span>
                <span class="sandwich"></span>
            </button>
        </div>
        <div class="navigation-links">
            <ul class="navbar-list collapse">
                <li class="nav-item"><a class="nav-link" href="#" @click="showMenu">Home</a></li>
                <li class="nav-item"><a href="#aboutConverter" class="nav-link" @click="showMenu">Coinverter</a></li>
                <li class="nav-item"><a href="#tablePage" class="nav-link" @click="showMenu">Tabela de Cotações</a></li>
                <li class="nav-item"><a href="#aboutBitcoin" class="nav-link" @click="showMenu">Sobre Bitcoin</a></li>
            </ul>
            <ul class="navbar-list">
                <li class="nav-item">Tema Escuro:</li>
                <li class="nav-item" id="toggle-content">
                    <button type="button" class="toggle-darkmode" @click="darkmodeButton">
                        <span id="toggler"></span>
                        <span id="toggler-text">Off</span>
                    </button>
                </li>
            </ul>
        </div>
    </nav>    
</template>

<script>
export default {
    data(){
        return{
            clickButtonDarkmode: 0,
            clickButtonCollapseMenu: 0
        }
    },

    methods : {
        darkmodeButton(){
            const togglerBg = document.querySelector('.toggle-darkmode')
            const toggler = document.querySelector('#toggler')
            const togglerText = document.querySelector('#toggler-text')
            if(this.clickButtonDarkmode == 0){
                togglerBg.style.backgroundColor = 'green'
                toggler.style.left = '26px'
                togglerText.style.right = '24px'
                togglerText.innerHTML = 'On'
                this.clickButtonDarkmode = 1
            } else {
                toggler.style.left = '0%'
                togglerText.style.right = '0%'
                togglerBg.style.backgroundColor = 'red'
                togglerText.innerHTML = 'Off'
                this.clickButtonDarkmode = 0
            }
        },

        showMenu(){
            const menuCollapse = document.querySelector('.navigation-links')
            if(screen.availWidth <= 992){
            if(this.clickButtonCollapseMenu == 0){
                document.body.style.overflowY = 'hidden'
                menuCollapse.style.overflow = 'visible'
                menuCollapse.style.height = '92.5vh'
                this.clickButtonCollapseMenu = 1
            } else {
                document.body.style.overflowY = 'visible'
                menuCollapse.style.overflow = 'hidden'
                menuCollapse.style.height = '0'
                this.clickButtonCollapseMenu = 0
            }
            }
        }
    }
}
</script>

<style scoped>

nav {
    display: flex;
    padding: 2vh 4vh;
    align-items: center;
    justify-content: space-between;
}

.navbar-brand {
    display: flex;
    align-items: center;
    text-decoration: none;
    color: black;
}

.navbar-brand img{
    width: 5vh;
    margin-right: 10px;
}

.navbar-toggler {
    height: fit-content;
    border-radius: 3px;
    border: 1px solid var(--nav-link);
    background: transparent;
    display: none;
}

.sandwich {
    display: block;
    height: 5px;
    width: 30px;
    margin: 5px;
    background: var(--nav-link);
    border-radius: 5px;
}

.navigation-links {
    display: flex;
    padding: 1vh;
    width: 85%;
    justify-content: space-between;
    z-index: 100;
    background-color: var(--body-color);
}

.nav-item {
    margin: 0 15px;
}

.navbar-list {
    list-style: none;
    display: inline-flex;
    align-items: center;
}

.nav-link {
    color: var(--nav-link);
    text-decoration: none;
}

/*  Toggler DarkMode  */

.toggle-darkmode {
    display: flex;
    width: 50px;
    height: 25px;
    background: red;
    border: none;
    border-radius: 100px;
    cursor: pointer;
    align-items: center;
    justify-content: space-between;
    padding: 0 2px;
}

.toggle-darkmode:focus{
    outline: none;
}

#toggler {
    position: relative;
    display: block;
    width: 20px;
    left: 0%;
    height: 23px;
    background: white;
    border-radius: 100px;
    transition: left .4s ease;
}

#toggler-text {
    position: relative;
    display: block;
    color: white;
    margin: 0 2px;
    font-weight: bold;
    right: 0%;
}

/*  Responsive  */

@media (max-width: 992px){
    nav {
        flex-direction: column;
    }

    .responsive-menu {
        width: 90%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .navbar-toggler{
        display: block;
    }

    .navigation-links {
        flex-direction: column;
        overflow: hidden;
        height: 0;
        transition: .4s ease-in-out;
        width: 100vw;
    }

    .navbar-list {
        padding: 10px 0;
        justify-content: center;
        align-items: center;
    }

    .navbar-list.collapse {
        flex-direction: column;
    }

    .navbar-list.collapse li{
        margin: 10px 0;
    }
}

</style>