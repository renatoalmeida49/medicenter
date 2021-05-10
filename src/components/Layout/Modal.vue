<template>
  <div class="modal" v-show="value" @click="fecharModal($event)">
      <div class="modal__container">
        <slot name="header"></slot>
        <slot name="body"></slot>
        <slot name="footer"></slot>

    <button class="button" @click="close()">Cancelar</button>
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
.modal::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, .5);
    z-index: 2;
}

.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    padding: 60px;
    z-index: 2;
}

.modal__container {
    position: relative;
    z-index: 2;
    background: #fff;
    padding: 20px;
    margin: auto;
    max-width: max-content;
}
</style>