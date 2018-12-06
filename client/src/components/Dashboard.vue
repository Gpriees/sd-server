<template>
  <div class="hello">
    <!-- <h1>Welcome to regular users page</h1>
        <h2>{{ msg }}</h2>
        <h3>Tempestade: {{ alerts.tempestade ? 'fodeu' : 'de boa' }}</h3>
    <h3>Maré alta: {{ alerts.mareAlta ? 'vivo' : 'morto' }}</h3>-->
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
                <img
                  src="https://www.bitmag.com.br/wp-content/uploads/2016/06/tecnologiasaude-684x225.png"
                >
              </div>
              <div class="body">
                <p>Medicamento - nome</p>
                <p>Disponibilidade - true-false</p>
                <p>Local - endereço/unidade do posto de saude</p>
                <button class="button">Solicitar medicamento</button>
              </div>
            </div>
          </li>
        </ul>
      </div>

      <div class="container">
        <ul>
          <li>
            <div class="card receita">
              <div class="body">
                <h2>Medicamento - nome</h2>
                <p>tipo - capsula/xarope</p>
                <p>dosagem - uma capsula a cada 3 horas</p>
              </div>
            </div>
          </li>
        </ul>
      </div>
      <div class="container">
        <div class="card table">
          <table style="width:100%">
            <tr>
              <th>Nome</th>
              <th>Postos de Saude para retirada</th>
            </tr>
            <tr>
              <td>Doril</td>
              <td>Centro e Lagoa</td>
            </tr>
            <tr>
              <td>Outro</td>
              <td>Centro</td>
            </tr>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "The commoners",
      alerts: () => ({})
    };
  },
  methods: {
    requestAlerts() {
      this.$http
        .get("http://localhost:3000/alerts")
        .then(({ data, status }) => {
          if (status === 200) {
            this.alerts = data;
          }
        });
    },
    subscribeAlerts() {
      setInterval(this.requestAlerts, 3500);
    }
  },
  mounted() {
    this.subscribeAlerts();
  }
};
</script>

<style scoped>
h1,
h2 {
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

* {
  color: #000;
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
  background-color: #666;
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
.work .container ul {
  margin: 0;
  width: 100%;
}
.work .container ul li {
  margin: 0;
  width: 30%;
}
.card {
  border-radius: 5px;
  width: 100%;
  background-color: #fff;
}
.card .head {
  width: 100%;
}
.card .head img {
  max-width: 100%;
  border-radius: 5px 5px 0 0;
}
.card .body {
  padding: 0 10px;
}
.card.receita .body {
  padding: 10px;
}
.card .body button {
  width: 40%;
  text-align: center;
  line-height: normal;
  display: inline-block;
  padding: 10px 0;
  margin: 10px auto;
  font-size: 14px;
  background: #7da2d4;
  border: none;
  color: #fff;
  font-weight: 500;
  border-radius: 100px;
  cursor: pointer;
}
.card .button:hover {
  background-color: #00afff;
}

.card .button:focus {
  outline: 0;
}
.card.table {
  margin: 0 auto;
  max-width: 60%;
  padding: 10px;
}
.card.table th,
.card.table td {
  text-align: left;
}
.card.table th{
  height: 30px;
}
</style>
