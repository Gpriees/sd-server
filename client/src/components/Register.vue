<template>
    <div class="card">
        <h4>Register</h4>
        <form>
            <label for="name">Name</label>
            <div>
                <input id="name" type="text" v-model="name" required autofocus>
            </div>

            <label for="email" >E-Mail Address</label>
            <div>
                <input id="email" type="email" v-model="email" required>
            </div>

            <label for="password">Password</label>
            <div>
                <input id="password" type="password" v-model="password" required>
            </div>

            <label for="password-confirm">Confirm Password</label>
            <div>
                <input id="password-confirm" type="password" v-model="password_confirmation" required>
            </div>

            <label for="password-confirm">Is this an administrator account?</label>
            <div>
                <select v-model="isAdmin">
                    <option value=1>Yes</option>
                    <option value=0>No</option>
                </select>
            </div>

            <div>
                <button type="submit" @click="handleSubmit">
                    Register
                </button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
  props: ['nextUrl'],
  data () {
    return {
      name: '',
      email: '',
      password: '',
      password_confirmation: '',
      isAdmin: null
    }
  },
  methods: {
    handleSubmit (e) {
      e.preventDefault()

      if (this.password === this.password_confirmation && this.password.length > 0) {
        const url = `http://localhost:3000/register${this.isAdmin ? '-admin' : ''}`
        this.$http.post(url, {
          name: this.name,
          email: this.email,
          password: this.password,
          isAdmin: this.isAdmin
        })
          .then(response => {
            localStorage.setItem('user', JSON.stringify(response.data.user))
            localStorage.setItem('jwt', response.data.token)

            if (localStorage.getItem('jwt') != null) {
              this.$emit('loggedIn')
              if (this.$route.params.nextUrl != null) {
                this.$router.push(this.$route.params.nextUrl)
              } else {
                this.$router.push('/')
              }
            }
          })
          .catch(error => {
            console.error(error)
          })
      } else {
        this.password = ''
        this.passwordConfirm = ''

        return alert('Passwords do not match')
      }
    }
  }
}
</script>

<style scoped>
.card {
  border-radius: 5px;
  width: 20%;
  background-color: #fff;
  display: inline-block;
  margin: 0 auto;
  padding: 20px 30px;
  vertical-align: middle;
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 1px 6px rgba(0,0,0,0.23);
}
.card label {
  margin: 10px 0 0;
  display: block;
}
.card button {
  margin: 10px 0 0;
  width: auto;
  height: 30px;
  background: white;
}
</style>
