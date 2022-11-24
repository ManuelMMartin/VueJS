<template>

  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Personas</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <FormularioPersona @add-persona="agregarPersona" />
        <div v-if="personas.length < 1" class="alert alert-info" role="alert">
          No hay ninguna persona en la base de datos
        </div>
        <TablaPersonas :personas="personas" @delete-persona="eliminarPersona" @editar-persona='actualizarPersona' />
      </div>
    </div>
  </div>
</template>

<script>
import TablaPersonas from '@/components/TablaPersonas.vue'
import FormularioPersona from './components/FormularioPersona.vue';

export default {
  name: 'App',
  components: {
    TablaPersonas,
    FormularioPersona
  },
  data() {
    return {
      personas: [
        {
          id: 1,
          nombre: 'Jon',
          apellido: 'Nieve',
          email: 'jon@email.com',
        },
        {
          id: 2,
          nombre: 'Tyrion',
          apellido: 'Lannister',
          email: 'tyrion@email.com',
        },
        {
          id: 3,
          nombre: 'Daenerys',
          apellido: 'Targaryen',
          email: 'daenerys@email.com',
        },
      ],
    }
  },
  methods: {
    agregarPersona(persona) {
      this.personas = [...this.personas, persona]
    },
    eliminarPersona(id) {
      this.personas = this.personas.filter(persona => persona.id != id)
    },
    actualizarPersona(id, personaActulizada) {
      this.personas = this.personas.map(persona =>
        persona.id === id ? personaActulizada : persona
      )
    }
  }
}
</script>

<style>

</style>
