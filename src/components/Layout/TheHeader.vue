<template>
    <header>
        <div class="container">
            <div class="logo">
                <a href="">
                    <img src="@/assets/medilogo.png" />
                </a>
            </div>
            <div class="menu">
                <nav>
                    <div class="menuMobile" @click="menuMobile()">
                        <div class="mm_line"></div>
                        <div class="mm_line"></div>
                        <div class="mm_line"></div>
                    </div>
                    <ul>
                        <li><router-link to="/">Início</router-link></li>
                        <li><a href="#hospitais">Hospitais</a></li>
                        <li><a href="">Departamentos</a></li>
                        <li><a href="">Sobre</a></li>
                    </ul>
                </nav>
            </div>

        </div>
    </header>
</template>

<script>

export default {
    name: "TheHeader",
    components: {
        
    },
    data() {
        return {
            
        }
    },
    methods: {
        menuMobile() {
            document.querySelector(".menu nav ul").classList.toggle('flex')
        }
    }
}
</script>

<style scoped>
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

a.router-link-exact-active {
    background-color: #39AAE1;
    color: white;
    border-radius: 6px;
}

/* HEADER */

header {
	display: flex;
	justify-content: center;
	padding: 20px;
}

.logo {
	display: flex;
	align-items: center;
}

.menu {
	display: flex;
	align-items: center;
	margin-left: 20px;
}

nav ul,
nav li {
	list-style: none;
	margin: 0;
	padding: 0;
}

nav ul {
	display: flex;
}

nav a {
	display: block;
	padding: 15px;
	text-decoration: none;
	text-transform: uppercase;
	color: #727272;
}

nav .active a,
nav a:hover {
	background-color: #39AAE1;
	color: white;
	border-radius: 6px;
}

/* MENU MOBILE */

.menuMobile {
	display: none;
	width: 30px;
	height: 30px;
}

.mm_line {
	background-color: #39aae1;
	height: 3px;
}

/* STATES */

.flex {
	display: flex;
}

@media (max-width: 916px) {
	.container {
		flex-direction: column;
	}

	#banner h1 {
		max-width: 100%;
		font-size: 2.81rem;
	}

	#banner h2 {
		max-width: 75%;
	}

	.menu {
		margin-top: 15px;
		justify-content: center;
	}
}

@media (max-width: 600px) {
	header .container {
		flex-direction: row;
	}

	#geral .container {
		flex-direction: column;
		padding: 0px;
	}

	nav ul {
		flex-direction: column;
		display: none;
		position: absolute;
		left: 0;
		width: 100%;
		background-color: white;
	}

	header {
		height: auto;
		padding: 0px;
	}

	.logo {
		padding: 20px;
	}

	.menuMobile {
		display: flex;
		flex-direction: column;
		justify-content: space-around;
	}
}
</style>