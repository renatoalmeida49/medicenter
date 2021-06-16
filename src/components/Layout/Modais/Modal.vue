<template>
    <div
        class="modal"
        v-show="value"
        @click="fecharModal($event)"
    >
        <div class="modal__container">
            <component
                :is="component"
                :info="info"
                @input="close()"
            />
        </div>
    </div>
</template>

<script>
export default {
    name: "Modal",
    props: {
        value: {
            required: true
        },
        typeComponent: {
            required: true
        },
        info: {
            required: false
        }
    },
    data() {
        return {
            component: {}
        }
    },
    mounted() {
        this.component = () => import(`./Views/${this.typeComponent}`)
    },
    methods: {
        close() {
            this.$emit("input", !this.value)
        },
        fecharModal(event) {
            if(event.target === event.currentTarget)
                this.$emit("input", !this.value)
        },
        
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