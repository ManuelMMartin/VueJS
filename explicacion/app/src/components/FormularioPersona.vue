<template>
   <div id="formulario-persona">
      <form @submit.prevent="enviarFormulario">
         <div class="container">
            <div class="row">
               <div class="col-md-4">
                  <div class="form-group">
                     <label>Nombre</label>
                     <input type="text" class="form-control" v-model="persona.nombre"
                        :class="{ 'is-invalid': procesando && validoNombre }" @focus="resetEstado" ref="nombre"
                        @keypress="resetEstado" />
                  </div>
               </div>
               <div class="col-md-4">
                  <div class="form-group">
                     <label>Apellido</label>
                     <input type="text" class="form-control" v-model="persona.apellido"
                        :class="{ 'is-invalid': procesando && validoApellido }" @focus="resetEstado" />
                  </div>
               </div>
               <div class="col-md-4">
                  <div class="form-group">
                     <label>Email</label>
                     <input type="email" class="form-control" v-model="persona.email"
                        :class="{ 'is-invalid': procesando && validoEmail }" @focus="resetEstado" />
                  </div>
               </div>
            </div>
            <div class="row">
               <div class="col-md-4">
                  <div class="form-group">
                     <button class="btn btn-primary">Añadir persona</button>
                  </div>
               </div>
            </div>
         </div>
         <div class="container">
            <div class="row">
               <div class="col-md-12">
                  <div v-if="error & procesando" class="alert alert-danger" role="alert">
                     debes rellenar todos los campos!
                  </div>
                  <div v-if="correcto" class="alert alert-success" role="alert">
                     Persona añadida correctamente
                  </div>
               </div>
            </div>
         </div>
      </form>
   </div>
</template>
<script>
export default {
   name: 'formulario-persona',
   data() {
      return {
         procesando: false,
         error: false,
         correcto: false,
         persona: {
            nombre: '',
            apellido: '',
            email: '',
         },
      }
   },
   methods: {

      enviarFormulario() {
         this.procesando = true
         this.resetEstado()
         if (this.validoNombre || this.validoApellido || this.validoEmail) {
            this.error = true
            return
         }
         this.$emit('add-persona', this.persona)
         this.$refs.nombre.focus()
         this.error = false
         this.correcto = true
         this.procesando = false

         this.persona = {
            nombre: '',
            apellido: '',
            email: ''
         }
      },
      resetEstado() {
         this.error = false
         this.correcto = false
      }
   },
   computed: {
      validoNombre() {
         return this.persona.nombre.length < 1
      },
      validoApellido() {
         return this.persona.apellido.length < 1
      },
      validoEmail() {
         return this.persona.email.length < 1
      }
   }
}
</script>
<style scoped>
form {
   margin-bottom: 2rem;
}
</style>