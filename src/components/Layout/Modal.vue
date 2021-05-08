<template>
  <div class="modal" v-show="value" @click="fecharModal($event)">
      <div class="modal__container">
        <slot name="header"></slot>
        <slot name="body"></slot>
        <slot name="footer"></slot>

        <button @click="close()">Cancelar</button>
      </div>
  </div>
</template>

<script>
export default {
    name: "Modal",
    props: {
        value: {
            required: true
        }
    },
    methods: {
        close() {
            this.$emit("input", !this.value)
        },
        fecharModal(event) {
            if(event.target === event.currentTarget)
                this.$emit("input", !this.value)
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

            this.close()
        }
    }
}
</script>

<style scoped>
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
</style>