<template>
  <div class="main">
    <div class="bg__image bg__image--left">
      <img src="@/assets/images/bg-left-top.png" alt="">
    </div>
    <div class="bg__image bg__image--right">
      <img src="@/assets/images/bg-right-down.png" alt="">
    </div>
  
    <p class="subtitle">find your block</p>
    <h1 class="title">Encontre os <strong>melhores blocos</strong><br /> de carnaval de 2023</h1>
  
    <div class="container__wrapper">
        <StatesInput :items="states" :selectState="selectState" icon="search" placeholder="Pesquise por nome"/>
        <CitiesInput :items="cities" :selectCity="selectCity" icon="pin" placeholder="Selecione uma cidade" />
        <ButtonComponent label="BUSCAR AGORA" />
    </div>

  </div>
</template>

<script>
import StatesInput from './States.vue';
import CitiesInput from './Cities.vue';
import ButtonComponent from './ButtonComponent.vue';

export default {
  components: { StatesInput, ButtonComponent, CitiesInput },
  data() {
    return {
      selectedState: '',
      selectedCity: '',
      states: [],
      cities: [],
      total: 0,
      city: {},
    }
  },
  async mounted() {
        const { geonames: states } = await (await fetch('http://www.geonames.org/childrenJSON?geonameId=3469034')).json()
        this.states = states
  },
  methods: {
    async searchCity(value) {
      if (!value) return;

      const { geonames: cities, totalResultsCount: total } = await (await fetch(`http://www.geonames.org/childrenJSON?geonameId=${value}`)).json()
      this.cities = cities
      this.total = total
    },
    async getCityInfo(value) {
      if (!value) return;

      const { geonames: city } = await (await fetch(`http://www.geonames.org/childrenJSON?geonameId=${value}`)).json()
      this.city = city[0]
    },
    selectState(value) {
      this.selectedState = value
    },
    selectCity(value) {
      this.selectedCity = value
    }
  },
  watch: {
    selectedState(newValue) {
      this.searchCity(newValue)
    },
    selectedCity(newValue) {
      this.getCityInfo(newValue)
    }
  }
}
</script>

<style scoped lang="scss">

.bg__image {
  position: absolute; 

  &--left {
    left: 0px;
    top: 0px;
  }

  &--right {
    right: 0;
    bottom: 0;
  }
}

.main {
  background: var(--primary-light);
  height: 532px;
  text-align: center;
  padding-top: 100px;
}

.container__wrapper {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  background-color: var(--vt-c-white);
  border: 1px solid var(--vt-c-text-dark-2);
  border-radius: 10px;
  padding: 40px;
  gap: 24px;
  width: 60%;
  margin: 0 auto;
}

.subtitle {
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--secondary);
}

.title {
  font-weight: 700;
  font-size: 48px;
  margin-bottom: 40px;

  strong {
    color: var(--primary);
    font-weight: 700;
  }
}
</style>
