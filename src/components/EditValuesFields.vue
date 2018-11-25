<template>
  <b-container class="bv-example-row">
    <div>
      <form @submit="onSubmit">
        <b-form-select v-model="form.name" :options="options" class="mb-3" />
        <b-form-input type="text" v-model="form.share_value" required placeholder="Enter value"></b-form-input>
        <b-button type="submit" variant="primary">Atualizar</b-button>
      </form>
      <b-alert variant="success" :show="showDismissibleAlert">Success update</b-alert>
    </div>
  </b-container>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      showDismissibleAlert: false,
      form: {
        name: '',
        share_value: ''
      },
      options: [
        { value: null, text: 'Please select an option' },
        { value: 'PETR4', text: 'PETR4' },
        { value: 'QUAL3', text: 'QUAL3' },
        { value: 'RADL3', text: 'RADL3' },
        { value: 'RAIL3', text: 'RAIL3' },
        { value: 'RENT3', text: 'RENT3' }
      ]
    }
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      let payload = JSON.stringify(this.form)
      axios.get(`http://127.0.0.1:3000/send_data`, {payload}).then((res) => {
        this.showDismissibleAlert = true
      })
    }
  }
}
</script>
