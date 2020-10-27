<template>
  <div id="app">
    <Form @onFormSubmit="onSubmit"/>
    <FruitList ref = 'listInstance' @updateSubmit="updateFruit" @refreshList="assignGet" @deleteSubmit="deleteFruit"/>
  </div>
</template>

<script>
import Form from './components/Form.vue'
import FruitList from './components/FruitList.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Form,
    FruitList
  },
  data() {
    return {
      url: "https://taskb-ilikefruits.herokuapp.com/api/fruits",
      fruits:[],
      show: false
    }
  },
  methods:{
    getFruitPromise(){
      return axios.get(this.url).then(response => {
        this.response = response.data.data
        console.log(this.response)
        return this.response
      })
    },
    assignGet(){
      console.log("starting get request")
      this.show=true
      this.getFruitPromise().then(data=> {
        this.fruits = data
        this.$refs.listInstance.fruits = data
      })
      console.log(this.fruits)
      this.show=false
    },
    onSubmit(data){
      alert(JSON.stringify(data))
      axios.post(this.url, {name:data.name, color:data.color, taste: data.taste})
      this.assignGet()
    },
    updateFruit(data){
      alert("Edited " + JSON.stringify(data))
      axios.put(this.url + "/" + data.id, {name:data.name, color:data.color, taste:data.taste})
      this.assignGet()
    },
    deleteFruit(data){
      alert("Deleted " + JSON.stringify(data))
      axios.delete(this.url + "/" + data.id)
      this.assignGet()
    },
    //setList function no longer in use (it was an attempt at fixing the parent-child prop reactivity)
    setList(fruitArray) {
      var fruit
      for (fruit in fruitArray){
        const newFruit = {'_id': fruit._id, 'name':fruit.name, 'color':fruit.color, 'taste':fruit.taste}
        this.fruits.push(newFruit)
      }
    }
  },
  mounted: function () {
    this.$nextTick(function () {
      this.assignGet()
      // Code that will run only after the
      // entire view has been rendered
    })
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
