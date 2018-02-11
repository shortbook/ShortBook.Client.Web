<template>
  <div>
    <b-form @submit="onSubmit">
      <b-form-group id="inputGroupEmail"
                    label="电子邮件"
                    label-for="inputEmail"
                    description="注册时登录的电子邮件地址。">
        <b-form-input id="inputEmail"
                      type="email"
                      v-model="form.email"
                      required
                      placeholder="example@shortbook.com">
        </b-form-input>
      </b-form-group>
      <b-form-group id="inputGroupPassword"
                    label="登录密码"
                    label-for="inputPassword">
        <b-form-input id="inputPassword"
                      type="password"
                      v-model="form.password"
                      required
                      placeholder="">
        </b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">登录</b-button>
      <b-button disabled :to="Register" variant="primary">注册</b-button>
    </b-form>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Login',
  data () {
    return {
      form: {
        email: '',
        password: ''
      }
    }
  },
  methods: {
    onSubmit (evt) {
      axios
        .post('http://localhost:5000/api/login', {
          email: this.form.email,
          password: this.form.password
        })
        .then(response => {
          alert(response.data)
        })
        .catch(e => {
          if (e.response) {
            alert(e.response.data)
          } else {
            alert(e.message)
          }
          this.errors.push(e)
        })
    }
  }
}
</script>
