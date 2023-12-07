<template>
  <!-- ======= Header/Navbar ======= -->
  <AppHeader></AppHeader>
  <!-- End Header/Navbar -->
  <main>
    <!-- ======= Intro ======= -->
    <section class="c-intro">
      <div class="container">
        <div class="row">
          <div class="col-12">
            <div class="c-intro__border">
              <h1 class="c-intro__title">Panden te koop</h1>
              <span class="u-color-text">De Panne en omgeving</span>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Intro -->

    <!-- Filter in component-->
    <section>
      <Filtering :filterData="filterData" :filters="filters" @zoekOpnieuw="filterHouses"></Filtering>
    </section>
    <!-- End filter in component-->

    <!-- ======= Property Grid ======= -->

    <section>
      <div class="container">
        <div v-if="loading" class="row">
          <Skeleton></Skeleton>
        </div>

        <!--<div v-if="loading" class="c-loader">
          <div class="c-loader__bar"></div>
          <div class="c-loader__bar"></div>
          <div class="c-loader__bar"></div>
        </div>-->

        <div v-else class="row">
          <!-- Panden in component -->
          <Houses :houses="houses"></Houses>
        </div>
      </div>
      <!-- End panden in component -->
    </section>
    <!-- End Property Grid -->
  </main>

  <!-- ======= Footer ======= -->
  <AppFooter></AppFooter>
  <!-- End  Footer -->
</template>

<script>
import { ref } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import Filtering from "./components/Filtering.vue";
import Houses from "./components/Houses.vue";
import Skeleton from "./components/Skeleton.vue";

export default {
  components: {
    AppHeader,
    AppFooter,
    Filtering,
    Houses,
    Skeleton,
  },

  setup() {
    const houses = ref([]);
    const loading = ref(true);

    const filters = ref({
      city: [],
      hometypeid: undefined,
      priceMin: undefined,
      priceMax: undefined,
      bedrooms: undefined,
    });

    const filterData = ref({
      cities: [],
      homeTypes: [],
    });

    const getData = function (baseUrl) {
      return fetch(baseUrl).then(function (response) {
        return response.json();
      });
    };

    const getHouses = async function () {
      //const jsonData = await getData(`https://realestate-api.fgmnts.be/api/v1/homes`);

      const jsonData = await getData(`https://realestate-api.fgmnts.be/api/v1/homes/?nopagination=true`);
      //.then(function (response) {return response.json();})
      houses.value = jsonData.data;
      loading.value = false;
    };

    const fillFilter = async function () {
      const cities = await getData(`https://realestate-api.fgmnts.be/api/v1/cities`);
      filterData.value.cities = cities.data;
      const homeTypes = await getData(`https://realestate-api.fgmnts.be/api/v1/hometypes`);
      filterData.value.homeTypes = homeTypes.data;
    };
    const filterHouses = async function () {
      const baseUrl = "https://realestate-api.fgmnts.be/api/v1/homes/";
      const filterParams = {};

      // Add filters to the filterParams object only if they have values
      if (filters.value.city && filters.value.city.length > 0) {
        filterParams.city = filters.value.city.join(",");
      }
      if (filters.value.hometypeid !== undefined && filters.value.hometypeid !== "undefined") {
        filterParams.hometypeid = filters.value.hometypeid;
      }
      if (filters.value.priceMin !== undefined) {
        filterParams.startprice = filters.value.priceMin;
      }
      if (filters.value.priceMax !== undefined) {
        filterParams.endprice = filters.value.priceMax;
      }
      if (filters.value.bedrooms !== undefined && filters.value.bedrooms !== "undefined") {
        filterParams.bedrooms = filters.value.bedrooms;
      }

      const filterString = Object.entries(filterParams)
        .map(([key, value]) => `${key}=${encodeURIComponent(value)}`)
        .join("&");

      //console.log(`${baseUrl}search/?${filterString}&nopagination=true`);

      loading.value = true; // Zet het skeleton weer aan, want we gaan nieuwe data ophalen
      const { data } = await fetch(`${baseUrl}search/?${filterString}&nopagination=true`).then((r) => r.json());
      loading.value = false; // Zet het skeleton weer uit, want de nieuwe data is binnen

      houses.value = data;
    };

    getHouses();
    fillFilter();

    //teruggeven HTML
    return {
      loading,
      houses,
      filterData,
      filters,
      filterHouses,
    };
  },
};
</script>

<style lang="scss">
/*---------------------------------------/*
 # SETTINGS
/*---------------------------------------*/
$color-primary: #2eca6a;

/*---------------------------------------/*
 # ELEMENTS
/*---------------------------------------*/
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

/*---------------------------------------/*
 # COMPONENTS
/*---------------------------------------*/
.c-intro {
  padding: 9rem 0 3rem;

  &__border {
    padding: 1rem 0 1rem 2rem;
    border-left: 3px solid $color-primary;
  }
  &__title {
    font-weight: 600;
    font-size: 2.2rem;
  }
}

.c-loader {
  display: inline-block;
  position: relative;
  width: 5rem;
  height: 5rem;
  margin: 0 auto;

  &__bar {
    display: inline-block;
    position: absolute;
    left: 0.5rem;
    width: 1rem;
    background: $color-primary;
    -webkit-animation: loader 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
    animation: loader 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;

    &:nth-child(1) {
      left: 0.5rem;
      -webkit-animation-delay: -0.24s;
      animation-delay: -0.24s;
    }

    &:nth-child(2) {
      left: 2rem;
      -webkit-animation-delay: -0.12s;
      animation-delay: -0.12s;
    }

    &:nth-child(3) {
      left: 3.5rem;
      -webkit-animation-delay: 0;
      animation-delay: 0;
    }
  }
}

/*---------------------------------------/*
 # TOOLS
/*---------------------------------------*/
@-webkit-keyframes loader {
  0% {
    top: 0.5rem;
    height: 4rem;
  }
  50%,
  100% {
    top: 1.5rem;
    height: 2rem;
  }
}

@keyframes loader {
  0% {
    top: 0.5rem;
    height: 4rem;
  }
  50%,
  100% {
    top: 1.5rem;
    height: 2rem;
  }
}
</style>
