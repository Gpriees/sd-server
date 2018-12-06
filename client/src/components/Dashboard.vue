<template>
    <div class="hello">
        <!-- <h1>Welcome to regular users page</h1>
        <h2>{{ msg }}</h2>
        <h3>Tempestade: {{ alerts.tempestade ? 'fodeu' : 'de boa' }}</h3>
        <h3>Maré alta: {{ alerts.mareAlta ? 'vivo' : 'morto' }}</h3> -->
        <div class="menu">
          <button class="button">Historico de receitas medicas</button>
          <button class="button">Lista de medicamentos disponibilizados</button>
          <button class="button">Solicitar medicamento</button>
        </div>
        <div class="work">
          <div class="container">
            <ul>
              <li>
                <div class="card">
                  <div class="head">
                    <img src="data:image/jpeg;base64,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">
                  </div>
                  <div class="body">
                    <p>Medicamento</p>
                    <p>Disponibilidade</p>
                    <p>Local</p>
                    <button class="button">Solicitar medicamento</button>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
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

  .menu {
    position: fixed;
    top: 0;
    left: 0;
    width: 20%;
    height: 100vh;
    background-color: #333;
  }

  .menu .button {
    width: 90%;
    text-align: center;
    line-height: normal;
    display: block;
    padding: 10px 0;
    margin: 10px auto;
    font-size: 14px;
    background: #3e3e3e;
    border: none;
    color: #fff;
    font-weight: 500;      
  }

  .menu .button:hover {
    background-color: #666
  }

  .menu .button:focus {
    background-color: #666;
    outline: 0;
  }        

  .work {
    display: block;
    width: 80%;
    min-height: 100vh;
    background: #666;
    margin-left: calc(20% - 8px);
    position: absolute;
    top: 0;
  }
  .work .container {
    margin: 15px;
    display: flex;
    flex-flow: row wrap;
  }
  .work .container ul{
    margin: 0;
    width: 100%;
  }
  .work .container ul li{
    margin: 0;
    width: 30%;
  }
  .card {
    border-radius: 5px;
    width: 100%;
    background-color: #fff;
  }
  .card .head{
    width: 100%;
  }
  .card .head img{
    max-width: 100%;
    border-radius: 5px 5px 0 0;
  }
  .card .body button{
    width: 90%;
    text-align: center;
    line-height: normal;
    display: block;
    padding: 10px 0;
    margin: 10px auto;
    font-size: 14px;
    background: #3e3e3e;
    border: none;
    color: #fff;
    font-weight: 500; 
  }
</style>
