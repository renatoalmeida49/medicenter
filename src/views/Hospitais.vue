<template>
  <div>
      <TheGeneral> 
          <template v-slot:button>
              <button @click="modal = !modal">Novo hospital</button>

            <div class="modal" v-if="modal" @click="fecharModal($event)">
                <div class="modal__container">
                    <h2>Adicionar hospital</h2>

                    <form>
                        <label for="nome">Nome</label>
                        <input v-model="hospital.nome" type="text" name="nome" id="nome" required />

                        <label for="cep">CEP</label>
                        <input v-model="hospital.cep" type="text" name="cep" id="cep" />

                        <label for="endereco">Endereço</label>
                        <input v-model="hospital.endereco" type="text" name="endereco" id="endereco" />

                        <label for="bairro">Bairro</label>
                        <input v-model="hospital.bairro" type="text" name="bairro" id="bairro" />

                        <label for="cidade">Cidade</label>
                        <input v-model="hospital.cidade" type="text" name="cidade" id="cidade" />

                        <label for="estado">Estado</label>
                        <input v-model="hospital.estado" type="text" name="estado" id="estado" />

                        <label for="lat">Lat</label>
                        <input v-model="hospital.lat" type="text" name="lat" id="lat" />

                        <label for="long">Long</label>
                        <input v-model="hospital.long" type="text" name="long" id="long" />

                        <label for="info">Informações adicionais</label>
                        <textarea v-model="hospital.informacoes" name="info" id="info" rows="8"></textarea>
                        
                        <div>
                            <button @click="adicionar()">Adicionar</button>
                            <button @click="modal = false">Cancelar</button>
                        </div>
                    </form>
                </div>
            </div>
          </template>
      </TheGeneral>
  </div>
</template>

<script>
import TheGeneral from "@/components/Home/TheGeneral"

export default {
    name: "Hospitais",
    components: {
        TheGeneral
    },
    data() {
        return {
            modal: false,
            hospital: {
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
        fecharModal(event) {
            if(event.target === event.currentTarget)
                this.modal = false
        },
        adicionar() {
            fetch('https://getpantry.cloud/apiv1/pantry/e79d83be-93de-41de-8dff-60da1c35938f/basket/hospitais', {
                method: 'POST',
                mode: 'cors',
                cache: 'no-cache',
                credentials: 'same-origin',
                headers: {
                    'Content-Type': 'application/json'
                },
                redirect: 'follow',
                referrerPolicy: 'no-referrer',
                body: this.hospital
            })
                .then(data => {
                    console.log(data)
                })
        }
    }
}
</script>

<style scoped>
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
    position: absolute;
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
    max-width: 320px;
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
}

form label {
    margin-top: 1rem;
}

form div {
    display: flex;
    justify-content: space-between;
}
</style>