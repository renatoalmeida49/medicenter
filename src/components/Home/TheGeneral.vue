<template>
    <section id="hospitais">
        <div class="container">
            <section>
                <div class="widget">
                    <div class="widget_title">
                        <div class="widget_title_text">Nossos hospitais</div>
                        <div class="widget_title_bar"></div>
                        
                        <button class="button" @click="openModal = !openModal">Novo hospital</button>

                        <Modal v-model="openModal" typeComponent="AdicionarHospital"/>
                    </div>

                    <div class="widget_body flex">
                        <div
                            v-for="hospital, id in baskets"
                            :key="id"
                            class="hospital"
                        >
                            <h2><img src="@/assets/icons/hospital.png" height="64" />{{hospital.nome}}</h2>
                            <p class="hospital-address"><img src="@/assets/icons/address.png" height="16" />{{hospital.endereco}}</p>
                            
                            <button class="hospital__options" @click="menuOptions($event)">
                                <div class="dot"></div>
                                <div class="dot"></div>
                                <div class="dot"></div>
                            </button>

                            <div class="hospital__options-menu">
                                <ul>
                                    <li>Editar</li>
                                    <li @click="excluir(hospital.id)">Excluir</li>
                                </ul>
                            </div>

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
import Modal from "@/components/Layout/Modais/Modal.vue"

export default {
    name: "TheGeneral",
    components: {
        Modal,
    },
    data() {
        return {
            baskets: [],
            hospitais: [],
            openModal: false
        }
    },
    methods: {
        newHospital() {
            this.openModal = !this.openModal
        },
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
        menuOptions(event) {
            console.log("clicou")
            if(event.target.classList.contains('dot')) {
                event.target.parentElement.nextSibling.classList.toggle('flex')
            } else {
                event.target.nextSibling.classList.toggle('flex')
            }
        },
        excluir(id) {
            fetch(`https://getpantry.cloud/apiv1/pantry/e79d83be-93de-41de-8dff-60da1c35938f/basket/${id}`, {
                method: 'DELETE',
                headers: {
                    'Content-Type': 'application/json; charset=UTF-8'
                }
            })
                .then(() => {
                    this.baskets = []
                    this.getHospitais()
                })
        }
    },
    watch: {
        openModal() {
            this.baskets = []
            this.getHospitais()
        }
    },
    created() {
        this.getHospitais()
    }
}
</script>

<style>
.button {
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

.button:hover {
    background: #fff;
    color: #39AAE1;
    border: 1px solid #39AAE1;
}

/* SECTION GERAL */

#hospitais {
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
}

#hospitais section {
	flex: 2;
}

#hospitais aside {
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
.flex {
	display: flex;
	flex-wrap: wrap;
    flex-direction: column;
}

/* HOSPITAL */

.hospital {
    background: #fff;
    margin: 5px 0;
    padding: 1rem;
    border-radius: 4px;
    position: relative;
    z-index: 1;
}

.hospital__options {
    position: absolute;
    display: flex;
    top: 10%;
    right: 2%;
    cursor: pointer;
    border: none;
    background: transparent;
}

.dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: #2c3e50;
    margin: 3px;
}

.hospital__options-menu {
    display: none;
    position: absolute;
    top: 22%;
    right: 2%;
    text-align: right;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.2);
    border-radius: 8px;;
}

.hospital__options-menu ul {
    list-style: none;
    font-weight: 700;
}

.hospital__options-menu li {
    padding: 5px;
    margin: 0 5px;
    cursor: pointer;
}

.hospital__options-menu li:hover {
    transform: scale(1.05);
}

.flex {
    display: flex;
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

@media (max-width: 460px) {
    .hospital-group {
        flex-direction: column;
    }

    .hospital-group p {
        margin: 5px 0;
    }
}
</style>