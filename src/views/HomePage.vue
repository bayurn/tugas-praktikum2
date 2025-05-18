<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Tugas 2 - Ionic Vue</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div id="container">
        <div class="btn-action">
          <ion-button @click="fetchData">Get Data</ion-button>
        </div>

        <div class="wrapper-table">
          <ion-grid>
            <ion-row class="head-table">
              <ion-col>Name</ion-col>
              <ion-col>Symbol</ion-col>
              <ion-col>Harga USD</ion-col>
            </ion-row>
            <ion-row v-for="currency in dataCurrencyArr" :key="currency.id">
              <ion-col>{{ currency.name }}</ion-col>
              <ion-col>{{ currency.symbol }}</ion-col>
              <ion-col>{{ currency.price_usd }}</ion-col>
            </ion-row>
          </ion-grid>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
export default {
  data() {
    return {
      dataCurrencyArr: [],
    };
  },
  methods: {
    fetchData() {
      fetch('https://api.coinlore.net/api/tickers/', {
        method: 'GET',
      })
        .then((res) => {
          res.json().then((data) => {
            this.dataCurrencyArr = data.data.slice(0, 10);
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>

<style scoped>
#container {
  font-size: 14px;
}

.btn-action {
  color: white;
  text-align: center;
  margin-top: 16px;
}

.wrapper-table {
  margin-top: 16px;
  padding: 4px;
}

ion-grid {
  border: 1px solid black;
  padding: 0;
}

ion-row {
  width: 100%;
  height: auto;
  text-align: center;
  align-items: center;
}

ion-row.head-table {
  border-bottom: 1px solid;
}

ion-col {
  padding: 8px;
}
</style>
