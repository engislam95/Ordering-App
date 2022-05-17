<template>
  <div class="bg-white">
    <div>
      <div
        class="relative z-40 lg:hidden"
        role="dialog"
        aria-modal="true"
        v-if="showSide"
      >
        <div class="fixed inset-0 bg-black bg-opacity-25"></div>
        <div class="fixed inset-0 flex z-40">
          <div
            class="ml-auto relative max-w-xs w-full h-full bg-white shadow-xl py-4 pb-12 flex flex-col overflow-y-auto"
          >
            <div class="px-4 flex items-center justify-between">
              <button
                type="button"
                class="-mr-2 w-10 h-10 bg-white p-2 rounded-md flex items-center justify-center text-gray-400"
                @click="showSide = false"
              >
                <span class="sr-only">Close menu</span>
                <svg
                  class="h-6 w-6"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="2"
                  stroke="currentColor"
                  aria-hidden="true"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>

            <!-- side order place -->
            <form class="mt-4 border-t border-gray-200">
              <div class="pointer-events-auto">
                <div class="flex h-full flex-col bg-white shadow-xl rounded-xl">
                  <div class="flex-1 overflow-y-auto py-6 px-4 sm:px-6">
                    <div class="flex items-start justify-center mb-5">
                      <h2
                        class="text-lg font-medium text-gray-900"
                        id="slide-over-title"
                      >
                        Order Summery
                      </h2>
                    </div>
                    <div class="py-8 border-t border-gray-200">
                      <div class="flow-root">
                        <ul role="list" class="-my-6">
                          <li
                            class="flex py-6"
                            v-for="product in addedProducts"
                            :key="product.id"
                          >
                            <div class="flex flex-1 flex-col">
                              <div>
                                <div
                                  class="flex justify-between items-baseline font-medium text-gray-900"
                                >
                                  <h5 class="text-xs text-gray-600">
                                    <span class="font-bold"
                                      >{{ product.quantity }}X
                                    </span>
                                    Throwback Hip Bag
                                  </h5>
                                  <p class="ml-4 text-xs font-bold">
                                    {{ product.Price }} SAR
                                  </p>
                                </div>
                              </div>
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>

                  <div class="border-t border-gray-200 py-6 px-4 sm:px-6">
                    <div
                      class="flex justify-between text-base font-medium text-gray-900"
                    >
                      <p>Total</p>
                      <p class="font-bold">{{ calcSum }} SAR</p>
                    </div>
                    <div class="mt-6">
                      <button
                        type="button"
                        :disabled="addedProducts.length < 1"
                        class=" rounded-md border border-transparent bg-indigo-600 px-6 py-3 text-base font-medium text-white shadow-sm hover:bg-indigo-700"
                        @click="placeOrder"
                      >
                        Place Order
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>

      <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div
          class="relative z-10 flex items-baseline justify-between pt-24 pb-6 border-b border-gray-200"
        >
          <h1 class="text-4xl font-extrabold tracking-tight text-gray-900">
            Ordering App
          </h1>

          <div class="flex items-center">
            <button
              type="button"
              class="p-2 -m-2 ml-4 sm:ml-6 text-gray-400 hover:text-gray-500 lg:hidden"
              @click="showSide = true"
            >
              <span class="sr-only">Filters</span>
              <!-- Heroicon name: solid/filter -->
              <svg
                class="w-5 h-5"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M3 3a1 1 0 011-1h12a1 1 0 011 1v3a1 1 0 01-.293.707L12 11.414V15a1 1 0 01-.293.707l-2 2A1 1 0 018 17v-5.586L3.293 6.707A1 1 0 013 6V3z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>
          </div>
        </div>

        <section aria-labelledby="products-heading" class="pt-6 pb-24">
          <h2 id="products-heading" class="sr-only">Products</h2>

          <div class="grid grid-cols-1 lg:grid-cols-4 gap-x-8 gap-y-10">
            <!-- order summary -->
            <form class="hidden lg:block">
              <div class="pointer-events-auto">
                <div class="flex h-full flex-col bg-white shadow-xl rounded-xl">
                  <div class="flex-1 overflow-y-auto py-6 px-4 sm:px-6">
                    <div class="flex items-start justify-center mb-5">
                      <h2
                        class="text-lg font-medium text-gray-900"
                        id="slide-over-title"
                      >
                        Order Summery
                      </h2>
                    </div>
                    <div class="py-8 border-t border-gray-200">
                      <div class="flow-root">
                        <ul role="list" class="-my-6">
                          <li
                            class="flex py-6"
                            v-for="product in addedProducts"
                            :key="product.id"
                          >
                            <div class="flex flex-1 flex-col">
                              <div>
                                <div
                                  class="flex justify-between items-baseline font-medium text-gray-900"
                                >
                                  <h5 class="text-xs text-gray-600">
                                    <span class="font-bold"
                                      >{{ product.quantity }}X
                                    </span>
                                    Throwback Hip Bag
                                  </h5>
                                  <p class="ml-4 text-xs font-bold">
                                    {{ product.Price }} SAR
                                  </p>
                                </div>
                              </div>
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>

                  <div class="border-t border-gray-200 py-6 px-4 sm:px-6">
                    <div
                      class="flex justify-between text-base font-medium text-gray-900"
                    >
                      <p>Total</p>
                      <p class="font-bold">{{ calcSum }} SAR</p>
                    </div>
                    <div class="mt-6">
                      <button
                        type="button"
                        :disabled="addedProducts.length < 1"
                        class=" rounded-md border border-transparent bg-indigo-600 px-6 py-3 text-base font-medium text-white shadow-sm hover:bg-indigo-700 "
                        @click="placeOrder"
                      >
                        Place Order
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </form>

            <!-- Product grid -->
            <div
              class="lg:col-span-3 bg-white shadow-xl rounded-xl h-100 lg:h-full"
            >
              <div
                class="mt-6 grid grid-cols-1 gap-y-10 gap-x-6 sm:grid-cols-2 lg:grid-cols-4 xl:gap-x-8"
              >
                <div
                  class="group relative p-5"
                  v-for="product in products"
                  :key="product.id"
                >
                  <ProductView
                    :product="product"
                    @orderSummary="getOrderSummary"
                  />
                </div>
              </div>
            </div>
          </div>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
import ProductView from "./ProductView.vue";

export default {
  name: "HomeView",
  components: {
    ProductView,
  },

  data() {
    return {
      products: [],
      addedProducts: [],
      showSide: false,
      alertOpen: false,
      alertText: "",
    };
  },
  mounted() {
    this.$http
      .get("https://627796e22f94a1d7061016b2.mockapi.io/api/v1/products")
      .then((response) => {
        this.products = response.data;
        console.log(response.data);
      });
  },
  computed: {
    calcSum() {
      let total = 0;
      this.addedProducts.forEach((item) => {
        total += parseInt(item.Price);
      });
      return total;
    },
  },
  methods: {
    getOrderSummary(product) {
      const check_index = this.addedProducts.findIndex(
        (item) => item.id === product.id
      );
      if (check_index !== -1) {
        this.addedProducts[check_index].quantity++;
        this.addedProducts[check_index].Price =
          parseInt(this.addedProducts[check_index].Price) +
          parseInt(product.Price);
      } else {
        this.addedProducts.push({ ...product, quantity: 1 });
      }
           this.$swal({
            position: "top",
            icon: "success",
            title: "Order Added successfully",
            showConfirmButton: false,
            timer: 1500,
          });
    },

    placeOrder() {
      let productsPayload = this.addedProducts.map(function (item) {
        return {
          id: item.id,
          quantity: item.quantity,
        };
      });
      this.$http
        .post(
          "https://627796e22f94a1d7061016b2.mockapi.io/api/v1/orders",
          productsPayload
        )
        .then((response) => {
          console.log(response);
          this.$swal({
            position: "top",
            icon: "success",
            title: "Order Placed successfully",
            showConfirmButton: false,
            timer: 1500,
          });
        });
    },
  },
};
</script>

<style scoped></style>
