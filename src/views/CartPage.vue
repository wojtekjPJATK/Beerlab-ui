<template>
  <v-container fluid class="pa-0">
    <v-row justify="center" align="center">
      <v-img width="100%" max-height="300px" src="@/assets/koszyk.jpeg">
      </v-img>
    </v-row>
    <v-row
      justify="center"
      v-if="
        order.orderItemsDto === undefined || order.orderItemsDto.length === 0
      "
    >
      <v-card class="text-center ma-4 elevation-12" color="orange lighten-2">
        <v-card-title>
          Aktualnie nie masz nic w zamówieniu!
        </v-card-title>
      </v-card>
    </v-row>
    <v-row v-else justify="center">
      <div class="align-center">
        <v-row
          justify="center"
          v-for="(orderItem, index) in order.orderItemsDto"
          :key="index"
          cols="12"
          sm="6"
          md="4"
          lg="3"
        >
          <BeerCartCard :orderItem="orderItem" :order="order"></BeerCartCard>
        </v-row>
        <v-card class="ma-5 justify-center orange lighten-2 elevation-12">
          <v-list-item>
            <v-list-item-content
              class="justify-center headline font-weight-bold "
            >
              Podsumowanie
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-content class="justify-center text-center">
              <h3>Suma: {{ order.totalPrice }} <v-icon large>mdi-beer</v-icon></h3>

            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-content class="align-center">
              <v-card-actions class="justify-center">
                <v-btn @click="confirmOrder(1)" rounded color="green" dark>
                  Zapłać kuflami
                </v-btn>
                <v-btn @click="confirmOrder(2)" rounded color="green" dark>
                  Zapłać przy barze
                </v-btn>
              </v-card-actions>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </div>
    </v-row>
  </v-container>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import BeerCartCard from "./components/BeerCartCard";
export default {
  name: "CartPage",
  data() {
    return {};
  },
  computed: {
    ...mapGetters({ order: "userActualOrder", user: "user" })
  },
  methods: {
    ...mapActions([
      "setOrderStatus",
      "fetchUserActualOrder",
      "reduceQuantity",
      "deleteItemFromOrder",
      "addToCart",
      "increaseAmount",
      "confirmOrder"
    ])
  },
  created() {
    this.fetchUserActualOrder();
  },
  components: {
    BeerCartCard
  }
};
</script>

<style scoped>
div {
  margin-bottom: 10px;
}
</style>
