<template>

  <section class="multiple-choice">
    <div class="jumbotron">
      <h2>MultipleChoice</h2>
      <hr>
      <table class="table table-striped table-dark table-bordered">
          <tr >
            <th>Número de pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr v-for="(p,index) in preguntas" :key="index">
            <td v-for="(colName,i) in getColumsNames" :key="i">{{p[colName]}}</td>
          </tr>
      </table>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'multiple-choice',
    props: [],
    mounted () {

    },
    data () {
      return {
        preguntas : [
          { numero: 1, respuestas: ['c'] },
          { numero: 2, respuestas: ['c'] },
          { numero: 3, respuestas: ['a','b'] },
        ]   
      }
    },
    methods: {

    },
    computed: {
      getColumsNames(){
        return Object.keys(this.preguntas[0])
      }
    }
}


</script>

<style scoped>
.multiple-choice {

}
.jumbotron {
  background-color: lightskyblue;
  color:white;
}
</style>
