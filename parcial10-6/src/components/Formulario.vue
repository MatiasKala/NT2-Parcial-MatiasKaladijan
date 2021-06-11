/* eslint-disable no-constant-condition */
/* eslint-disable no-constant-condition */
<template>

  <section class="formulario">
    <div class="jumbotron">
      <h2>Formulario</h2>
      <hr>

      <vue-form :state="formState" @submit.prevent="enviar()">
        
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <br>
          <input 
          type="text"
          class="form-control"
          autocomplete="off"
          id="nombre"
          name="nombre"
          v-model="formData.nombre"
          :minlength="lengthMin"
          :maxlength="lengthMax"
          no-espacios
          required
          >
          <field-messages name="nombre" show="$dirty">
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo
            </div>            
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como mínimo {{ lengthMin }} caracteres
            </div>     
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>            
            <div v-if="formData.nombre.length == lengthMax" class="alert alert-warning mt-1">
              Este campo debe tener como máximo {{ lengthMax }} caracteres
            </div>   
          </field-messages>
        </validate>

        <br>

        <validate tag="div">
          <label for="apellido">Apellido</label>
          <br>
          <input 
          type="text"
          class="form-control"
          autocomplete="off"
          id="apellido"
          name="apellido"
          v-model="formData.apellido"
          :minlength="lengthMin"
          :maxlength="lengthMax"
          no-espacios
          required
          >
          <field-messages name="apellido" show="$dirty">
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo
            </div>            
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como mínimo {{ lengthMin }} caracteres
            </div>     
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>            
            <div v-if="formData.apellido.length == lengthMax" class="alert alert-warning mt-1">
              Este campo debe tener como máximo {{ lengthMax }} caracteres
            </div>   
          </field-messages>
        </validate>

        <br>

        <validate tag="div">
          <label for="nota">Nota</label>
          <br>
          <input 
          type="number"
          class="form-control"
          autocomplete="off"
          id="nota"
          name="nota"
          v-model.number="formData.nota"
          :min="notaMin"
          :max="notaMax"
          required
          >
          <field-messages name="nota" show="$dirty">        
            <div slot="min" class="alert alert-danger mt-1">
              Este campo admite valores de {{ notaMin }} a {{notaMax}}
            </div>     
            <div slot="max" class="alert alert-danger mt-1">
              Este campo admite valores de {{ notaMin }} a {{notaMax}}
            </div>     
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>            
          </field-messages>
        </validate>
        
        <button class="btn btn-info my-3" :disabled="formState.$invalid" type="submit">Enviar</button>

      </vue-form >

      
      <hr>
      <br>

      <h1><u>Tabla Alumnos</u></h1>
      <br>
      <div v-if="alumnos.length>0">
        <table class="table table-dark  m-2">
          <tr>
            <th>Nombre</th>
            <th>Nota</th>
          </tr>
          <tr v-for="(alumno,index) in alumnos" :key="index">
            <td>{{alumno.nombre+' '+alumno.apellido}}</td>
            <td :style="getEstilo(alumno.nota)">{{alumno.nota}}</td>
          </tr>
          <tr :style="getEstilo(promedioTotal)">
            <td>Promedio Total</td>
            <td>{{promedioTotal}}</td>
          </tr>
        </table>
      </div>
    </div>


  </section>

</template>

<script>

  export default  {
    name: 'formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        alumnos : [],
        formData : this.getInicialData(),
        formState : {},
        lengthMin : 3,
        lengthMax : 15,
        notaMin : 0,
        notaMax : 10,
      }
    },
    filters:{
      esNota:(v)=>{return isNaN(v)? v: v},
    },
    methods: {
      getEstilo(valor) {
        if(valor>=0 && valor<4) return {color: 'red'}
        if(valor>=4 && valor<7) return {color: 'yellow'}
        return {color: 'rgba(51, 255, 54, 1)'}
      },
      getInicialData(){
        return {
          nombre: '',
          apellido: '',
          nota: '',
        }
      },
      enviar(){
        this.alumnos.push({...this.formData})
        console.log(this.alumnos);
        this.formData=this.getInicialData()
        this.formState._reset() 
      },
    },
    computed: {
      getCols() {
        return Object.keys(this.alumnos[0])
      },
      promedioTotal(){
        // if(this.alumnos.length>0){
        //   return 0
        // }
        let contador=0
        let acum=0
        this.alumnos.forEach(function(a) {
          contador++
          acum += a.nota
          console.log(acum);
        });
        return acum/contador
      }
    }
}


</script>

<style scoped>
.jumbotron {
  background-color: darkblue;
  color:white;
}
hr{
  background-color: lightcyan;
}
</style>
