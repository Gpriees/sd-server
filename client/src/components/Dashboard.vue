<template>
    <div class="hello">
        <h1>Welcome to regular users page</h1>
        <h2>{{ msg }}</h2>
        <h3>Tempestade: {{ alerts.tempestade ? 'fodeu' : 'de boa' }}</h3>
        <h3>Maré alta: {{ alerts.mareAlta ? 'vivo' : 'morto' }}</h3>
    </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'The commoners',
      alerts: () => ({})
    }
  },
  methods: {
    requestAlerts () {
      this.$http.get('http://localhost:3000/alerts')
        .then(({ data, status }) => {
          if (status === 200) {
            this.alerts = data
          }
        })
    },
    subscribeAlerts () {
      setInterval(this.requestAlerts, 3500)
    }
  },
  mounted () {
    this.subscribeAlerts()
  }
}
</script>

<style scoped>
    h1, h2 {
        font-weight: normal;
    }
    ul {
        list-style-type: none;
        padding: 0;
    }
    li {
        display: inline-block;
        margin: 0 10px;
    }
    a {
        color: #42b983;
    }
</style>
