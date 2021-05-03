<template>
    <section id="geral">
        <div class="container">
            <section>
                <div class="widget">
                    <div class="widget_title">
                        <div class="widget_title_text">Nossos hospitais</div>
                        <div class="widget_title_bar"></div>
                        
                        <button @click="modal = !modal">Novo hospital</button>

                        <div class="modal" v-if="modal" @click="fecharModal($event)">
                            <div class="modal__container">
                                <h2>Adicionar hospital</h2>

                                <form method="POST">
                                    <div class="form-group fg1">
                                        <label for="nome">Nome</label>
                                        <input v-model="hospital.nome" type="text" name="nome" id="nome" required />

                                        <label for="cep">CEP</label>
                                        <input v-model="hospital.cep" type="text" name="cep" id="cep" />

                                        <label for="endereco">Endereço</label>
                                        <input v-model="hospital.endereco" type="text" name="endereco" id="endereco" />
                                    </div>
                                    
                                    <div class="form-group fg2">
                                        <div>
                                            <label for="bairro">Bairro</label>
                                            <input v-model="hospital.bairro" type="text" name="bairro" id="bairro" />
                                        </div>

                                        <div>
                                            <label for="cidade">Cidade</label>
                                            <input v-model="hospital.cidade" type="text" name="cidade" id="cidade" />
                                        </div>

                                        <div>
                                            <label for="estado">Estado</label>
                                            <input v-model="hospital.estado" type="text" name="estado" id="estado" />
                                        </div>
                                    </div>

                                    <div class="form-group fg2">
                                        <div>
                                            <label for="lat">Lat</label>
                                            <input v-model="hospital.lat" type="text" name="lat" id="lat" />
                                        </div>

                                        <div>
                                            <label for="long">Long</label>
                                            <input v-model="hospital.long" type="text" name="long" id="long" />
                                        </div>
                                    </div>

                                    <label for="info">Informações adicionais</label>
                                    <textarea v-model="hospital.informacoes" name="info" id="info" rows="8"></textarea>
                                    
                                    <div class="form-group">
                                        <button @click.prevent="adicionar()">Adicionar</button>
                                        <button @click="modal = false">Cancelar</button>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>

                    <div class="widget_body flex">
                        <div
                            v-for="hospital, id in baskets"
                            :key="id"
                            class="hospital"
                        >
                            <h2><img src="@/assets/icons/hospital.png" height="64" />{{hospital.nome}}</h2>
                            <p class="hospital-address"><img src="@/assets/icons/address.png" height="16" />{{hospital.endereco}}</p>

                            <div class="hospital-group">
                                <p>{{hospital.cep}}</p>
                                <p>{{hospital.bairro}}</p>
                                <p class="hospital-city">
                                    <img src="@/assets/icons/city.png" height="32px"/>
                                    {{hospital.cidade}} - {{hospital.estado}}
                                </p>
                            </div>
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
            hospitais: [],
            modal: false,
            hospital: {
                id: '',
                nome: '',
                cep: '',
                endereco: '',
                bairro: '',
                cidade: '',
                estado: '',
                lat: '',
                long: '',
                informacoes: ''
            }
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
        },
        fecharModal(event) {
            if(event.target === event.currentTarget)
                this.modal = false
        },
        adicionar() {
            this.hospital.id = Date.now()

            //fetch('http://localhost:3000/hospitais', {
            fetch(`https://getpantry.cloud/apiv1/pantry/e79d83be-93de-41de-8dff-60da1c35938f/basket/${this.hospital.id}`, {
                method: 'POST',
                body: JSON.stringify(this.hospital),
                headers: {
                    'Content-Type': 'application/json; charset=UTF-8'
                }
            })
                .then(data => {
                    console.log(data)
                    this.reset()
                })
        },
        reset() {
            this.modal = false

            this.hospital.id = ''
            this.hospital.nome = ''
            this.hospital.cep = ''
            this.hospital.endereco = ''
            this.hospital.bairro = ''
            this.hospital.cidade = ''
            this.hospital.estado = ''
            this.hospital.lat = ''
            this.hospital.long = ''
            this.hospital.informacoes = ''
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

/* MODAL */

button {
    display: block;
	padding: 15px;
	text-transform: uppercase;
    background-color: #39AAE1;
	color: white;
	border-radius: 6px;
    border: 1px solid transparent;
    margin: 5px 0;
    cursor: pointer;
}

button:hover {
    background: #fff;
    color: #39AAE1;
    border: 1px solid #39AAE1;
}

.modal::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, .5);
}

.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    padding: 60px;
}

.modal__container {
    position: relative;
    z-index: 100;
    background: #fff;
    padding: 20px;
    margin: auto;
    max-width: max-content;
}

.modal form {
    display: flex;
    flex-direction: column;
}

form input,
form textarea {
    padding: 0.5rem;
    font-size: 1rem;
    border: 1px solid white;
    border-radius: 4px;
    box-shadow: 0 4px 8px rgba(20, 60, 90, 0.2);
    cursor: pointer;
}

form input:hover,
form textarea:hover {
    border: 1px solid #39AAE1;
}

form input:focus,
form textarea:focus {
    outline: none;
    border-color: #39AAE1;
}

form label {
    margin-top: 1rem;
}

.form-group {
    display: flex;
    justify-content: space-between;
}

.fg1 {
    display: flex;
    flex-direction: column;
    margin: 8px 0;
}

.fg2 {
    display: flex;
    flex-wrap: wrap;
    margin: 8px 0;
}

.fg2 div {
    display: flex;
    flex-direction: column;
}

/* HOSPITAL */

.hospital {
    background: #fff;
    margin: 5px 0;
    padding: 1rem;
    border-radius: 4px;
}

.hospital img {
    margin-right: 16px;
}

.hospital h2 {
    margin-bottom: 16px;
    display: flex;
    align-items: center;
}

.hospital-address {
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    font-weight: 700;
    font-size: 1.3rem;
}

.hospital-group {
    display: flex;
    justify-content: space-around;
}

.hospital-city {
    display: flex;
    align-items: center;
}
</style>