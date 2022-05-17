<template>
  <div>
    <div
      class="w-full min-h-30 bg-gray-200 aspect-w-1 aspect-h-1 rounded-xl overflow-hidden lg:h-30 lg:aspect-none cursor-pointer"
      @click="toggleModal()"
    >
      <img
        :src="product.image"
        alt="product image"
        class="w-full h-full object-center object-contain lg:w-full lg:h-full"
      />
      <p class="text-sm p-3 font-medium text-gray-900 text-center">
        {{ product.Price }} SAR
      </p>
    </div>
    <div
      v-if="showModal"
      class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex"
    >
      <div class="relative z-10" role="dialog" aria-modal="true">
        <div
          class="hidden fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity md:block"
        ></div>
        <div class="fixed z-10 inset-0 overflow-y-auto">
          <div
            class="flex items-stretch md:items-center justify-center min-h-full text-center md:px-2 lg:px-4"
          >
            <div
              class="flex text-base text-left transform transition w-full md:max-w-2xl md:px-4 md:my-8 lg:max-w-4xl"
            >
              <div
                class="w-full relative flex items-center bg-white px-4 pt-14 pb-8 overflow-hidden shadow-2xl sm:px-6 sm:pt-8 md:p-6 lg:p-8"
              >
                <button
                  @click="toggleModal()"
                  type="button"
                  class="absolute top-4 right-4 text-gray-400 hover:text-gray-500 sm:top-8 sm:right-6 md:top-6 md:right-6 lg:top-8 lg:right-8"
                >
                  <span class="sr-only">Close</span>
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

                <div
                  class="w-full grid grid-cols-1 gap-y-8 gap-x-6 items-start sm:grid-cols-12 lg:gap-x-8"
                >
                  <div
                    class="aspect-w-2 aspect-h-3 rounded-lg bg-gray-100 overflow-hidden sm:col-span-4 lg:col-span-5"
                  >
                    <img
                      :src="product.image"
                      alt="Two each of gray, white, and black shirts arranged on table."
                      class="object-center object-cover"
                    />
                  </div>
                  <div class="sm:col-span-8 lg:col-span-7">
                    <div
                      class="mt-10 flex justify-between text-base font-medium text-gray-900"
                    >
                      <h3>
                        {{ product.name }}
                      </h3>
                      <p class="ml-4">{{ product.Price }} SAR</p>
                    </div>
                    <p class="mt-1 text-sm text-gray-500">
                      {{ product.description }}
                    </p>
                    <button
                      type="button"
                      class="mt-6 w-full bg-indigo-600 border border-transparent rounded-md py-3 px-8 flex items-center justify-center text-base font-medium text-white hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                      @click="addProduct(product)"
                    >
                      Add to order
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="showModal" class="opacity-25 fixed inset-0 z-40 bg-black"></div>
  </div>
</template>

<script>
export default {
  name: "ProductView",
  data() {
    return {
      showModal: false,
      addedProducts: [],
    };
  },
  props: {
    product: Object,
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },
    addProduct(product) {
      this.$emit("orderSummary", product);
      this.toggleModal();
    },
  },
};
</script>

<style></style>
