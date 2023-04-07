<template>
  <div class="shop">
    <h1>shop</h1>
    <div v-for="item in items" :key="item.id">
      {{ item.name }} {{ item.price }}$
      <button @click="addtocart(item)">add to cart</button>
    </div>
    <h1>cart</h1>
    <div class="cart" v-for="item in cart">
      {{ item.name }} {{ item.price }}$
      <button @click="increment(item)">increment</button>
      <button @click="decrement(item)">decrement</button>
    </div>
    <button @click="removefromcart(item in cart)">remove from cart</button>
    <p>{{ numItems }}</p>
    <h4>Total Price: {{ cartSum }}$</h4>
    <button @click="checkout">checkout</button>
  </div>
</template>

<script>
export default {
  name: 'shop',
  data() {
    return {
      items: [
        {
          id: 1,
          name: 'iphone',
          price: 1000,
          quantity: 1,
        },
        {
          id: 2,
          name: 'galaxy',
          price: 2000,
          quantity: 1,
        },
      ],
      cart: [],
    };
  },
  methods: {
    addtocart(item) {
      let itemSearch = this.cart.filter(function (value) {
        if (item.id == value.id) {
          return value;
        }
      });

      if (itemSearch.length == 0) {
        this.cart.push(item);
      } else {
        let index = this.cart.indexOf(itemSearch[0]);
        this.cart[index].quantity = item.quantity;
        item.quantity++;
      }
      console.log(this.cart);
    },
    removefromcart(item) {
      this.cart.splice(item);
    },
    increment(item) {
      let itemSearch = this.cart.filter(function (value) {
        if (item.id == value.id) {
          return value;
        }
      });

      let index = this.cart.indexOf(itemSearch[0]);
      this.cart[index].quantity = item.quantity;
      item.quantity++;
    },
    decrement(item) {
      let cartItemIndex = this.cart.findIndex((x) => x === item);
      if (cartItemIndex >= 0) {
        this.cart.splice(cartItemIndex, 1);
      }
    },
    checkout() {
      console.log(JSON.parse(JSON.stringify(this.cart)));
    },
  },
  computed: {
    cartSum() {
      let total = 0;
      this.cart.forEach((item) => {
        total += item.price * item.quantity;
      });
      return total;
    },
    numItems() {
      let sum = 0;
      this.cart.forEach((item) => {
        sum += item.quantity;
      });
      return sum;
    },
  },
};
</script>

<style>
body {
  text-align: center;
}
</style>
