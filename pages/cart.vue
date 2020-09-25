<template>
  <main class="cart container">
    <h2>Your Cart</h2>

    <section v-if="cart.length">
      <table>
        <thead>
          <tr>
            <th>Item</th>
            <th>Add Ons</th>
            <th>Amount</th>
            <th>Total Price</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in cart" :key="item.id">
            <td>
              {{ item.item }}
              <span v-if="item.options">- {{ item.options }}</span>
            </td>
            <td>
              <span v-for="addon in item.addOns" :key="addon" class="comma">{{
                addon
              }}</span>
            </td>
            <td>{{ item.count }}</td>
            <td>{{ item.combinedPrice }}</td>
          </tr>
          <tr>
            <td colspan="3"></td>
            <td class="total">Total: ${{ totalPrice.toFixed(2) }}</td>
          </tr>
        </tbody>
      </table>
      <button @click="emptyCart">Empty Cart</button>
    </section>
  </main>
</template>

<script>
import AppEmptyCart from "@/components/AppEmptyCart.vue";
export default {
  components: {
    AppEmptyCart
  },
  methods: {
    emptyCart() {
      this.$store.commit("removeCart");
    }
  },
  computed: {
    cart() {
      return this.$store.state.cart;
    },
    totalPrice() {
      return this.$store.getters.totalPrice;
    }
  }
};
</script>

<style lang="scss" scoped>
button {
  float: right;
}
</style>
