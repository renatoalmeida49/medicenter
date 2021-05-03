<template>
    <section id="banner">
        <div class="container column">
            <h1>Medicenter</h1>
            <h2>Registrando e informando sobre os hospitais que possuem atendimento de emergência.</h2>

            <div class="banner_options">
            <div class="banner1">
                <h3>Casos de emergência</h3>
                <p class="banner_desc">Algum texto qualquer</p>
                <a href="">Leia mais</a>
            </div>

            <div class="banner2">
                <h3>Horários dos médicos</h3>
                <p class="banner_desc">Algum texto qualquer</p>
                <a href="">Leia mais</a>
            </div>
            
            <div class="banner3">
                <h3>Horário de funcionamento</h3>
                
                <div class="period">
                <div>Segunda - Sexta</div>
                <div>8.00 - 17.00</div>
                </div>
                <div class="period">
                <div>Sábado</div>
                <div>9.30 - 17.30</div>
                </div>
                <div class="period">
                <div>Domingo</div>
                <div>9.30 - 15.00</div>
                </div>
            </div>
            </div>
        </div>
	</section>
</template>

<script>
export default {

}
</script>

<style scoped>
    /* BANNER INICIAL */

#banner {
	display: flex;
	justify-content: center;
	background-image: url('../../assets/imgBanner.png');
	background-position: center;
	background-size: cover;
}

.column {
	flex-direction: column;
}

#banner h1 {
	color: white;
	font-size: 4.37rem;
	text-shadow: 0px 2px 0px #555555;
	margin: 10px 0 10px 0;
	padding: 1rem;
	max-width: 50%;
}

#banner h2 {
	color: white;
	font-size: 1.31rem;
	text-shadow: 0px 2px 0px #555555;
	margin: 10px 0 10px 0;
	padding: 1rem;
	max-width: 50%;
}

.banner_options {
	display: flex;
	flex-wrap: wrap;
	margin-top: 50px;
}

.banner1,
.banner2,
.banner3 {
	flex: 1;
	color: white;
	padding: 20px;
	box-shadow: 2px 2px 2px rgb(0 0 0 / 20%);
}

.banner1 {
	background-color: #39aae1;
	min-width: 210px;
}

.banner2 {
	background-color: #0079c7;
	min-width: 210px;
}

.banner3 {
	background-color: #2b4c99;
	min-width: 256px;
}

.banner_desc {
	font-size: 0.75rem;
	margin-top: 20px;
	margin-bottom: 20px;
}

.banner_options a {
	display: inline-block;
	border: 1px solid #FFFFFF;
	padding: 5px;
	color: #FFFFFF;
	font-size: 0.81rem;
	text-decoration: none;
	border-radius: 4px;
}

.banner1 a:hover {
	color: #39aae1;
	background-color: #fff;
}

.banner2 a:hover {
	color: #0079c7;
	background-color: #fff;
}

.banner3 h3 {
	margin-bottom: 10px;
}

.period {
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	border-bottom: 1px solid #266fc5;
	height: 35px;
	align-items: center;
}
</style>