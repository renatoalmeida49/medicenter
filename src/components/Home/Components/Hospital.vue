<template>
<div
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
</template>

<script>
export default {
    name: "Hospital",
    props: ["hospital"],
    methods: {
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
                    this.$emit('render')
                })
        }
    }
}
</script>

<style>

</style>