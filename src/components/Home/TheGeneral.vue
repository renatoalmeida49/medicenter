<template>
    <section id="geral">
        <div class="container">
            <section>
                <div class="widget">
                    <div class="widget_title">
                        <div class="widget_title_text">Nossos hospitais</div>
                        <div class="widget_title_bar"></div>
                        <slot name="button"></slot>
                    </div>

                    <div class="widget_body flex">
                        <div
                            v-for="hospital, id in baskets"
                            :key="id"
                        >
                            <h2>{{hospital.nome}}</h2>
                            <p>{{hospital.endereco}}</p>
                            <p>{{hospital.cep}}</p>
                            <p>{{hospital.estado}}</p>
                        </div>
                    </div>
                </div>
            </section>

            <aside>
                <div>
                    <div class="widget_title">
                        <div class="widget_title_text">Departments</div>
                        <div class="widget_title_bar"></div>
                    </div>
                    <div class="widget_body">
                        <div class="dp"></div>
                        <div class="dp"></div>
                        <div class="dp"></div>
                        <div class="dp"></div>
                        <div class="dp"></div>
                        <div class="dp"></div>
                    </div>
                </div>

                <div>
                    <div class="widget_title">
                        <div class="widget_title_text">Make an appointment</div>
                        <div class="widget_title_bar"></div>
                    </div>
                    <div>
                        <p>Texto para orientação de marcação</p>
                        <div class="period">
                            <div>Monday - Friday</div>
                            <div>8.00 - 17.00</div>
                        </div>
                        <div class="period">
                            <div>Saturday</div>
                            <div>9.30 - 17.30</div>
                        </div>
                        <div class="period">
                            <div>Sunday</div>
                            <div>9.30 - 15.00</div>
                        </div>
                    </div>
                </div>
            </aside>
        </div>
    </section>
</template>

<script>
export default {
    name: "TheGeneral",
    data() {
        return {
            baskets: [],
            hospitais: []
        }
    },
    methods: {
        async getHospitais() {
            await fetch('https://getpantry.cloud/apiv1/pantry/e79d83be-93de-41de-8dff-60da1c35938f')
                .then(data => data.json())
                .then(json => {
                    this.hospitais = json.baskets
                })

            this.getBasket()
        },
        getBasket() {
            this.hospitais.forEach(element => {
                fetch(`https://getpantry.cloud/apiv1/pantry/e79d83be-93de-41de-8dff-60da1c35938f/basket/${element}`)
                    .then(data => data.json())
                    .then(json => {
                        this.baskets.push(json)
                    })
            })
        }
    },
    created() {
        this.getHospitais()
    }
}
</script>

<style scoped>

/* SECTION GERAL */

#geral {
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
}

#geral section {
	flex: 2;
}

#geral aside {
	flex: 1;
}

.widget_title {
	margin-top: 30px;
	margin-bottom: 20px;
}

.widget_title_text {
	color: black;
	font-size: 1.31rem;
	font-weight: bold;
}

.widget_title_bar {
	width: 50px;
	height: 2px;
	background-color: #36a9e1;
	margin-top: 10px;
}

/* ASIDE */

.widget_body {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
}

.widget_body .dp {
	width: 155px;
	height: 145px;
	margin: 0 2px 2px 0;
	background-color: #39aae1;
}

/* GERAL SECTION */

article {
	flex: 1;
	min-width: 300px;
	margin: 5px;

	box-shadow: 2px 2px 2px rgb(0 0 0 / 20%);
    padding: 8px;
    border-radius: 4px;
    border: 1px solid rgba(0 0 0 / 20%);

	background: rgb(245, 244, 244);

	cursor: pointer;
}

article a {
	text-decoration: none;
}

article:hover {
	background: #fff;
}

article .news_posted_at {
	background-color: #2b4c99;
	color: white;
	font-size: 0.75rem;
	padding: 10px;
	margin-right: 2px;
	display: inline-block;
}

article .news_comments {
	background-color: #39AAE1;
	color: white;
	font-size: 0.75rem;
	padding: 10px;
	display: inline-block;
}

article .news_thumbnail {
	margin-top: 30px;
}

article .news_thumbnail img {
	height: auto;
}

article h2{
	margin-top: 25px;
	margin-bottom: 25px;
	color: black;
	font-weight: normal;
	font-size: 1.43rem;
}

article p {
	color: #5c5c5c;
	font-size: 0.87rem;
	line-height: 20px;
	margin-bottom: 30px;
}

.flex {
	display: flex;
	flex-wrap: wrap;
    flex-direction: column;
}
</style>