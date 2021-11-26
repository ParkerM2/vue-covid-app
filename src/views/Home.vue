<template>
  <main v-if="!loading">
    <DataTitle :dataDate="dataDate" :text="title"/>
    <DataBoxes :stats="status" />
    <CountrySelect :countries="countries" @get-country="getCountryData" />
    <button
        v-if="status.Country"
        class="bg-green-400 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
        @click="clearCountryData"
    >
    Clear Country
    </button>
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-400 text-3x1 mt-10 mb-6">
        Fetching Data
    </div>
    <img :src="require('../assets/hourglass.gif')" alt="hourglass loader" class="w-24 m-auto">
  </main>
</template>

<script>
import CountrySelect from '@/components/CountrySelect';
import DataBoxes from '@/components/DataBoxes';
import  { ref } from 'vue';
import DataTitle from '../components/DataTitle.vue';

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },

    setup() {
        const loading = ref(true);
        const title = ref('Global');
        const dataDate = ref('');
        const status =ref({});
        const countries = ref([]);

        const fetchCovidData = async () => {
            const res = await fetch('https://api.covid19api.com/summary');
            return await res.json();
        };

        const getCountryData = (country) => {
            status.value = country;
            title.value = country.Country;
        };

        const clearCountryData = async () => {
            baseSetup();
        };

        const baseSetup = async () => {
            const data = await fetchCovidData();

            dataDate.value = dataDate;
            status.value = data.Global;
            countries.value = data.Countries;
            loading.value = false;
            title.value = "Global";

        };

        baseSetup();

        return {
            loading,
            title,
            dataDate,
            status,
            countries,
            getCountryData,
            clearCountryData
        };
    }
};
</script>
