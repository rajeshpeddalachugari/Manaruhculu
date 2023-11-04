<script>
import Accordion from "primevue/accordion";
import AccordionTab from "primevue/accordiontab";
import logo from "./assets/logo1.svg";
import { menuItems } from "./data";

export default {
  components: {
    Accordion,
    AccordionTab,
  },
  data() {
    return {
      name: "Mana Ruchulu",
      mainLogo: logo,
      menuItems,
    };
  },
  methods: {
    getItemVariationNames(variations) { 
      const data = variations
        .map((item) => item.name)
        .filter((item) => item != undefined);
      return data;
    },
    getItemVariationPrices(variations) {
      return variations
        .map((item) =>item.variation_price)
        .filter((item) => item != undefined);
    },
  },
};
</script>
<template>
  <div class="flex flex-row items-center">
    <img :src="mainLogo" width="100" height="100" alt="main logo" />
    <h1 class="text-4xl font-bold font-serif text-orange-400">
      {{ name }}
    </h1>
  </div>
  <div class="flex justify-center pt-2 pb-2">
    <h3 class="text-xl font-bold font-serif">Our Menu</h3>
  </div>
  <Accordion :multiple="false" :activeIndex="[0]">
    <AccordionTab v-for="item in menuItems" :header="item.name">
      <table
        class="border-collapse w-full border border-slate-400 dark:border-slate-500 bg-white dark:bg-slate-800 text-sm shadow-sm"
      >
        <thead class="bg-slate-50 dark:bg-slate-700">
          <tr>
            <th class="table-header">Name</th>
            <th class="table-header">Price</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="menuItem in item.items">
            <td
              v-if="menuItem.Variation_name != null"
              class="table-data flex-col gap-2"
            >
              <p>{{ menuItem.name }}</p>
              <p>
                &#40;
                <span
                  v-for="(variationNames, index) in getItemVariationNames(
                    menuItem.variations
                  )"
                  >{{ index ? `/ ${variationNames} ` : `${variationNames} ` }}</span
                >
                &#41;
              </p>
            </td>
            <td v-else class="table-data">
              {{ menuItem.name }}
            </td>
            <td v-if="menuItem.Variation_name != null" class="table-data">
              <p>
                &#40;
                <span
                  v-for="(variationPrices, index) in getItemVariationPrices(
                    menuItem.variations
                  )"
                  >{{ index ? `/ ${variationPrices} ` : `${variationPrices} ` }}</span
                >
                &#41;
              </p>
            </td>
            <td v-else class="table-data">
              {{ menuItem.price }}
            </td>
          </tr>
        </tbody>
      </table>
    </AccordionTab>
  </Accordion>
</template>
