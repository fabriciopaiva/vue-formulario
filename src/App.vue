<template>
  <div id="app">

    <b-row>
      <b-col>
        <h2>Formulário de Testes com vue e bootstrap</h2>
        <b-form @submit="onSubmit" @reset="onReset" v-if="show">          
          <b-form-group
            id="exampleInputGroup1"
            label="Email address:"
            label-for="exampleInput1"
            description="We'll never share your email with anyone else."
          >
            <b-form-input
              id="exampleInput1"
              type="email"
              v-model="form.email"
              required
              placeholder="Enter email" />
          </b-form-group>

          <b-form-group 
            id="exampleInputGroup2"
            :invalid-feedback="invalidFeedback"
            :valid-feedback="validFeedback"
            :state="state"
            label="Your Name:" 
            label-for="exampleInput2">
            <b-form-input
              id="exampleInput2"
              type="text"
              :state="state"
              v-model="form.name"
              required
              placeholder="Enter name" />
          </b-form-group>

          <b-form-group id="exampleInputGroup3" label="Food:" label-for="exampleInput3">
            <b-form-select id="exampleInput3" :options="foods" required v-model="form.food" />
          </b-form-group>

          <b-form-group id="exampleGroup4">
            <b-form-checkbox-group v-model="form.checked" id="exampleChecks">
              <b-form-checkbox value="me">Check me out</b-form-checkbox>
              <b-form-checkbox value="that">Check that out</b-form-checkbox>
            </b-form-checkbox-group>
          </b-form-group>

          <b-button type="submit" variant="primary">Submit</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
      </b-col>
      <b-col>
        <h2>Resultado</h2>
        <b-row>
          <b-col>E-mail:</b-col>
          <b-col>{{ form.email }}</b-col>
        </b-row>
        <b-row>
          <b-col>Name:</b-col>
          <b-col>{{ form.name }}</b-col>
        </b-row>
        <b-row>
          <b-col>Food:</b-col>
          <b-col>{{ form.food }}</b-col>
        </b-row>
        <b-row>
          <b-col>Checks:</b-col>
          <b-col>{{ form.checked }}</b-col>
        </b-row>
      </b-col>
    </b-row>

  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    //HelloWorld
  },
  data() {
      return {
        form: {
          email: '',
          name: '',
          food: null,
          checked: []
        },
        foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        show: true
      }
    },
    computed: {
      state() {
        return this.form.name.length >= 4 ? true : false
      },
      invalidFeedback() {
        if (this.form.name.length > 4) {
          return ''
        } else if (this.form.name.length > 0) {
          return 'Enter at least 4 characters'
        } else {
          return 'Please enter something'
        }
      },
      validFeedback() {
        return this.state === true ? 'Thank you' : ''
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
        alert(JSON.stringify(this.form))
      },
      onReset(evt) {
        evt.preventDefault()
        /* Reset our form values */
        this.form.email = ''
        this.form.name = ''
        this.form.food = null
        this.form.checked = []
        /* Trick to reset/clear native browser form validation state */
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
