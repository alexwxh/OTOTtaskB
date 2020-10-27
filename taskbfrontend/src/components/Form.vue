<template>
    <div>
        <b-form inline>
            <b-input
                    id="name"
                    v-model="form.name"
                    class="mb-2 mr-sm-2 mb-sm-0"
                    placeholder="Fruit name"
                    required
            ></b-input>

            <b-input id="color"
                     v-model="form.color"
                     class="mb-2 mr-sm-2 mb-sm-0"
                     required
                     placeholder="Color"></b-input>

            <b-input
                    id="taste"
                    v-model="form.taste"
                    class="mb-2 mr-sm-2 mb-sm-0"
                    placeholder="Fruit taste"
            ></b-input>
            <b-button v-on:click="checkForm" variant="primary">Submit</b-button>
            <b-button @click="onReset" variant="danger">Reset</b-button>
        </b-form>
    </div>
</template>

<script>
    export default {
        name:'Form',
        data() {
            return {
                form: {
                    name: '',
                    color: '',
                    taste: ''
                },
                show: true
            }
        },
        methods: {
            onSubmit() {
                console.log('submitted')
                this.$emit("onFormSubmit", this.form)
                this.onReset()
            },
            onReset() {
                // Reset our form values
                this.form.name = ''
                this.form.color = ''
                this.form.taste = ''
            },
            checkForm(){
                console.log('form check')
                if (this.form.name && this.form.color){
                    this.onSubmit()
                }
                else {
                    alert("fields missing")
                }
            }
        }
    }
</script>
<style scoped>

</style>