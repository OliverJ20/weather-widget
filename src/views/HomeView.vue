<script setup lang="ts">
import TemperatureDisplay from "../components/TemperatureDisplay.vue";
</script>

<template>
  <main>
    <ul class="card-wrapper">
      <li class="card">
        <div class="wrapper">
          <dropdown
            class="my-dropdown-toggle"
            :options="options"
            :selected="selectedOption"
            v-on:updateOption="dropdownSelect"
            :placeholder="'Select an Item'"
          />
        </div>
        <div class="img-wrapper">
          <img
            v-bind:src="`http://openweathermap.org/img/w/${currentSelectedIcon}.png`"
            width="200"
            height="160"
            alt="weather"
          />
        </div>
        <TemperatureDisplay :msg="currentSelect?.main?.temp" />
      </li>
    </ul>
  </main>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import dropdown from "vue-dropdowns";
import axios from "axios";

/**
 * I broke the interface down into what I needed for the task,
 * the api does provide more information but I didn't feel the need to type it all out
 */
interface OpenWeather {
  weather: Array<Weather>;
  main: {
    temp: string;
  };
}
interface dropdownPayload {
  name: string;
}
interface Weather {
  id: number;
  main: string;
  description: string;
  icon: string;
}
export default defineComponent({
  components: {
    dropdown: dropdown,
  },
  data() {
    return {
      options: [
        {
          name: "Brisbane",
        },
        {
          name: "Sydney",
        },
        {
          name: "Melbourne",
        },
      ],
      selectedOption: {
        name: "Brisbane",
      },
      brisbaneWeather: {} as OpenWeather,
      sydneyWeather: {} as OpenWeather,
      melbourneWeather: {} as OpenWeather,
      currentSelect: {} as OpenWeather,
      brisbaneIcon: "",
      sydneyIcon: "",
      melbourneIcon: "",
      currentSelectedIcon: "",
    };
  },
  methods: {
    /**
     * Handles the switch logic when choosing between the three city options.
     * @param value
     */
    dropdownSelect(value: dropdownPayload) {
      this.selectedOption = value;

      switch (value.name) {
        case "Sydney":
          this.currentSelect = this.sydneyWeather;
          this.currentSelectedIcon = this.sydneyIcon;
          break;
        case "Melbourne":
          this.currentSelect = this.melbourneWeather;
          this.currentSelectedIcon = this.melbourneIcon;
          break;
        default:
          this.currentSelect = this.brisbaneWeather;
          this.currentSelectedIcon = this.brisbaneIcon;
      }
    },
    /**
     * Performs an axios get request to openweather api using the key stored in the env
     */
    async fetchBrisbaneWeather() {
      const brisbaneWeatherResponse = await axios.get<OpenWeather>(
        `https://api.openweathermap.org/data/2.5/weather?lat=-27.4679&lon=153.0281&units=metric&appid=${
          import.meta.env.VITE_WEATHER_API_KEY
        }`
      );
      this.brisbaneWeather = brisbaneWeatherResponse.data;
      this.brisbaneIcon = this.brisbaneWeather.weather[0].icon;
    },
    async fetchSydneyWeather() {
      const sydneyWeatherResponse = await axios.get<OpenWeather>(
        `https://api.openweathermap.org/data/2.5/weather?lat=-33.8679&lon=151.2073&units=metric&appid=${
          import.meta.env.VITE_WEATHER_API_KEY
        }`
      );
      this.sydneyWeather = sydneyWeatherResponse.data;
      this.sydneyIcon = this.sydneyWeather.weather[0].icon;
    },
    async fetchMelbourneWeather() {
      const melbourneWeatherResponse = await axios.get<OpenWeather>(
        `https://api.openweathermap.org/data/2.5/weather?lat=-37.814&lon=144.9633&units=metric&appid=${
          import.meta.env.VITE_WEATHER_API_KEY
        }`
      );
      this.melbourneWeather = melbourneWeatherResponse.data;
      this.melbourneIcon = this.melbourneWeather.weather[0].icon;
    },
  },
  async mounted() {
    await this.fetchBrisbaneWeather();
    await this.fetchSydneyWeather();
    await this.fetchMelbourneWeather();
    this.currentSelect = this.brisbaneWeather;
    this.currentSelectedIcon = this.brisbaneIcon;
  },
});
</script>
<style scoped>
.img-wrapper {
  margin-left: 20%;
  bottom: -25px;
}
.card {
  --card-gradient: rgba(0, 0, 0, 0.8);
  --card-gradient: #5e9ad9, #e271ad;
  --card-blend-mode: overlay;

  background-color: #fff;
  border-radius: 0.5rem;
  box-shadow: 0.05rem 0.1rem 0.3rem -0.03rem rgba(0, 0, 0, 0.45);
  padding-bottom: 1rem;
  background-image: linear-gradient(
    var(--card-gradient),
    white max(9.5rem, 27vh)
  );
  overflow: hidden;
}

.card-wrapper {
  list-style: none;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(30ch, 1fr));
  grid-gap: 1.5rem;
  max-width: 100vw;
  width: 400px;
  height: 380px;
  padding-left: 1rem;
  padding-right: 1rem;
}

.my-dropdown-toggle {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
  width: 368px;
  color: hsla(160, 100%, 37%, 1) !important;
  bottom: -10px;
}

:deep(.dropdown-menu > li > a) {
  color: hsla(160, 100%, 37%, 1) !important;
}
:deep(.dropdown-toggle) {
  color: hsl(164deg 91% 50%) !important;
}

:deep(.dropdown-menu) {
  top: 75px;
  font-weight: 500;
  font-size: 2.6rem;
  width: 368px !important;
}
</style>
