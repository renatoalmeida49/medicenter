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
                    <div class="menuMobile">
                        <div class="mm_line"></div>
                        <div class="mm_line"></div>
                        <div class="mm_line"></div>
                    </div>
                    <ul>
                        <li class="active"><a href="">HOME</a></li>
                        <li><a href="">HOME</a></li>
                        <li><a href="">HOME</a></li>
                        <li><a href="">HOME</a></li>
                        <li><a href="">HOME</a></li>
                        <li><a href="">HOME</a></li>
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
    }
}
</script>

<style scoped>
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

</style>