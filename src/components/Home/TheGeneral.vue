<template>
    <section id="hospitais">
        <div class="container">
            <section>
                <div class="widget">
                    <div class="widget_title">
                        <div class="widget_title_text">Nossos hospitais</div>
                        <div class="widget_title_bar"></div>
                        
                        <button @click="openModal = !openModal">Novo hospital</button>

                        <Modal v-model="openModal">
                            <template v-slot:header>
                                <h1>Adicionar hospital</h1>
                            </template>

                            <template v-slot:body>
                                <Form @newHospital="newHospital"/>
                            </template>

                            <template v-slot:footer>
                            </template>
                        </Modal>
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
import Modal from "@/components/Layout/Modal.vue"
import Form from "@/components/Home/Form.vue"

export default {
    name: "TheGeneral",
    components: {
        Modal,
        Form
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

<style scoped>

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