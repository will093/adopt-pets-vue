<template>
  <div class="home">
    <h1>Adopt a new best friends!</h1>
    {{ getAllCats.length }}
    {{ animalsCount }}

    <button @click="togglePetForm()" class="btn btn-primary">Add New Pet</button>

      <b-form @submit.prevent="handleSubmit" v-if="showPetForm">

        <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
          <b-form-input id="input-1" v-model="formData.name" required></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Species:" label-for="input-2">
          <b-form-select id="input-2" v-model="formData.species" :options="['cats', 'dogs']" required></b-form-select>
        </b-form-group>

      <b-form-group id="input-group-3" label="Age:" label-for="input-3">
        <b-form-input id="input-3" v-model="formData.age" required></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)

      // Reset form after submit
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
