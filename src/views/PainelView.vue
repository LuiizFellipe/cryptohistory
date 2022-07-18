<template>
  <div id="painel">
    <b-row class="mb-5">
      <b-col cols="8">
      <h1>{{ Titulo }}</h1>
      </b-col>
    <b-col cols="4">Cotacao do dollar: 
      <div v-for="x in APIJSON.slice(5, 6)" :key="x.id">
          {{ realBR.format(x.priceUsd * 5.42) }}
        </div>
    </b-col>
</b-row>
      <div class="text-center">
  <!-- <b-spinner label="Text Centered"></b-spinner> -->
</div>
    <b-row>
      <b-col>
        <div v-for="x in APIJSON.slice(0, 1)" :key="x.id">
          {{ x.symbol }}
          <img class="svg" src="../assets/img/transfer.svg" /> USD 
          <br />
          {{ dollarUS.format(x.priceUsd) }}
         
        </div>
        <div id="chart"></div>
      </b-col>
      <b-col>
        <div v-for="x in APIJSON.slice(1, 2)" :key="x.id">
          {{ x.symbol }}
          <img class="svg" src="../assets/img/transfer.svg" /> USD<br />
          {{ dollarUS.format(x.priceUsd) }}
        </div>
      </b-col>
      <b-col>
        <div v-for="x in APIJSON.slice(8,9)" :key="x.id">
          {{ x.symbol }}
          <img class="svg" src="../assets/img/transfer.svg" /> USD<br />
          {{ dollarUS.format(x.priceUsd) }}
        </div>
      </b-col>
      <b-col>
        <div v-for="x in APIJSON.slice(7, 8)" :key="x.id">
          {{ x.symbol }}
          <img class="svg" src="../assets/img/transfer.svg" /> USD<br />
          {{ dollarUS.format(x.priceUsd) }}
        </div></b-col
      >
    </b-row>
  </div>
</template>
<script>
import axios from "axios";
import moment from "moment";
const serv = "https://api.coincap.io/v2/assets";
const id = "bitcoin";
const history = serv + "/" + id + "/history?interval=d1";

export default {
  components: {},
  data() {
    return {
      Titulo: "Painel Atualizado",
      APIJSON: [],
      arrPrice: [],
      arrDate: [],
      chartOptions: {
        responsive: true,
      },
      dollarUS: Intl.NumberFormat("en-US", {
        style: "currency",
        currency: "USD",
      }),
      realBR: Intl.NumberFormat("pt-BR", {
        style: "currency",
        currency: "BRL",
      }),
    };
  },
  created() {
    // this.chart();
    this.getAPI();
  },
  methods: {
    async getAPI() {
      await axios({
        method: "GET",
        url: serv,
      })
        .then((API) => {
         // console.log(API);
          this.APIJSON = API.data.data;
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    async chart() {
      const { data } = await axios.get(history);
      // console.log(data.data)
      data.data.forEach((d) => {
        const dateConvert = moment(d.date, "YYYY-MM-DD").format("DD/MM/YYYY");
        const { priceUsd } = d;
        // this.arrDate.push(dateConvert);
        // this.arrPrice.push(priceUsd);

        this.arrPrice.push({ dateConvert, total: priceUsd });
        // console.log(this.arrPrice);
      });
    },
  },
};
</script>
<style>
@import url("../assets/painel.css");
</style>