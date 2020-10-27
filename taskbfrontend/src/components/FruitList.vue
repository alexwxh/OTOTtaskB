<template>
    <div>
        <b-table hover :items="fruits" :fields="fields" @row-clicked="updateListForm">
        </b-table>
        <b-button @click="$bvModal.show('editModal')" variant="info">Edit</b-button>
        <b-button @click="deleteForm" variant="danger">Delete</b-button>
        <b-button @click="refreshList" variant="danger">Refresh</b-button>
        <b-modal id = "editModal" hide-footer>
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
                        <b-button v-on:click="updateFruit" variant="primary">Submit</b-button>
                    </b-form>
                </div>
            </template>
        </b-modal>
    </div>
</template>

<script>
    export default {
        name: "FruitList",
        data() {
            return {
                fields: [
                    {
                        key: '_id',
                        label: 'Fruit ID',
                        sortable: true
                    },
                    {
                        key: 'name',
                        sortable: true
                    },
                    {
                        key: 'color',
                        sortable: false
                    },
                    {
                        key: 'taste',
                        sortable: false,
                    }
                ],
                items: [{
                    '_id': '5', 'name':'test'
                }],
                form: {
                    id:'',
                    name: '',
                    color: '',
                    taste: ''
                }
            }
        },
        props: {
            fruits: {
                type: Array
            }
        },
        methods: {
            updateListForm(item){
                this.form.id = item._id
                this.form.name = item.name
                this.form.color = item.color
                this.form.taste = item.taste
            },
            updateFruit(){
                this.$emit("updateSubmit", this.form)
                this.onReset()
            },
            onReset() {
                // Reset our form values
                this.form.name = ''
                this.form.color = ''
                this.form.taste = ''
            },
            deleteForm(){
                this.$emit("deleteSubmit", this.form)
            },
            refreshList(){
                console.log(this.fruits)
                this.$emit('refreshList')
            }
        }
    }
</script>

<style scoped>

</style>