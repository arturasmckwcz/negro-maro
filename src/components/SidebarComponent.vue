<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <button class="cart-close" @click="toggle">&times;</button>
      </h1>

      <div class="cart-body">
        <ProductsTableComponent
          :inventory="inventory"
          :items="cartContent"
          :handleButtonClick="deleteFromCart"
          :cart="true"
        />
        <table v-if="false" class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in cartContent" :key="item.id">
              <td><i :class="iconClassName(item)"></i></td>
              <td>{{ item.name }}</td>
              <td class="center">${{ item.price }}</td>
              <td class="center">{{ item.quantity }}</td>
              <td class="center">
                ${{ (item.quantity * item.price).toFixed(2) }}
              </td>
              <td class="center">
                <button
                  class="btn btn-light cart-remove"
                  @click="deleteFromCart(item.id)"
                >
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p class="center">
          <em v-if="cartContent.length === 0">No items in cart</em>
        </p>
        <div class="spread">
          <span><strong>Total:</strong> ${{ computedTotal.toFixed(2) }}</span>
          <button class="btn btn-light" @click="checkoutCart(cartContent)">
            Checkout
          </button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
import ProductsTableComponent from "@/components/ProductsTableComponent.vue";

export default {
  name: "SidebarComponent",
  components: { ProductsTableComponent },
  props: ["toggle", "cart", "inventory", "deleteFromCart", "checkoutCart"],
  methods: {
    iconClassName(item) {
      return `icofont-${item.icon} icofont-3x`;
    },
  },
  computed: {
    cartContent() {
      return Object.keys(this.cart).map((item) => {
        const product = this.inventory.find(({ id }) => id == item);
        return {
          quantity: this.cart[item],
          id: product.id,
          name: product.name,
          icon: product.icon,
          price: product.price.USD,
        };
      });
    },
    computedTotal() {
      return this.cartContent.reduce((result, item) => {
        return result + item.quantity * item.price;
      }, 0);
    },
  },
};
</script>
