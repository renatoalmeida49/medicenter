<template>
<div>
    <h1>Adicionar hospital</h1>
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

        <button class="button" @click.prevent="adicionar()">Adicionar</button>
    </form>
</div>
</template>

<script>

export default {
    name: "AdicionarHospital",
    data() {
        return {
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
            },
        }
    },
    methods: {
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
                .then(() => {
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

            this.$emit("input")
        }
    }
}
</script>

<style scoped>
form {
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
</style>