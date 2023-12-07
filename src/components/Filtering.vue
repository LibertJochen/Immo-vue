<template>
  <!-- ======= Search ======= -->
  <section>
    <div class="container mb-4">
      <div class="row">
        <div class="col-lg-3 col-md-6 mb-2">
          <div class="form-group mt-3">
            <label class="form-label" for="gemeente">Gemeentes</label>
            <select class="form-control" id="gemeente" name="city" v-model="filters.city" multiple @change="filterVeranderd">
              <option :value="undefined">Maak een keuze...</option>
              <option v-for="city in filterData.cities" :value="city.city">{{ city.city }}({{ city.number_of_homes }})</option>
            </select>
          </div>
        </div>
        <div class="col-lg-3 col-md-6 mb-2">
          <div class="form-group mt-3">
            <label class="form-label" for="type">Type</label>
            <select class="form-control" id="type" name="type" v-model="filters.hometypeid" @change="filterVeranderd">
              <option value="undefined">Maak een keuze...</option>
              <option v-for="homeType in filterData.homeTypes" :value="homeType.id">{{ homeType.description }}</option>
            </select>
          </div>
        </div>
        <div class="col-lg-3 col-md-6 mb-2 d-flex">
          <div class="c-input form-group mt-3 me-1">
            <label class="form-label" for="prijsmin">Prijs min.</label>
            <input class="form-control" type="number" step="50000" id="prijsmin" name="pricemin" v-model="filters.priceMin" @change="filterVeranderd" />
          </div>
          <div class="c-input form-group mt-3 ms-1">
            <label class="form-label" for="prijsmax">max.</label>
            <input class="form-control" type="number" step="50000" id="prijsmax" name="pricemax" v-model="filters.priceMax" @change="filterVeranderd" />
          </div>
        </div>
        <div class="col-lg-3 col-md-6 mb-2">
          <div class="form-group mt-3">
            <label class="form-label" for="opp">Slaapkamers min.</label>
            <select class="form-control" id="opp" name="bedrooms" v-model="filters.bedrooms" @change="filterVeranderd">
              <option value="undefined">Maak een keuze...</option>
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
            </select>
          </div>
        </div>
      </div>
    </div>
  </section>
  <!-- End Search -->
</template>

<script>
//1 Imports
import { ref } from "vue";
//2 Export
export default {
  //2.1 Emits
  emits: ["zoekOpnieuw"],
  //2.2 Props
  props: {
    filters: { type: Object, required: true },
    filterData: { type: Object, required: true },
  },
  //2.3 Setup
  setup(props, { emit }) {
    //2.6 Functies declareren
    const filterVeranderd = function () {
      //console.log(props.filters);
      emit("zoekOpnieuw");
    };
    return {
      filterVeranderd,
    };
  },
};
</script>

<style lang="scss">
/*---------------------------------------/*
 # SETTINGS
/*---------------------------------------*/
$color-gray-dark: #313131;
$color-white: #fff;
$color-primary: #2eca6a;
$color-gray-light: #f3f3f3;

/*---------------------------------------/*
 # GENERIC - BOOTSTRAP
/*---------------------------------------*/
.choices {
  &[data-type*="select-multiple"] &__inner,
  &[data-type*="text"] &__inner {
    cursor: default;
  }
  &__inner {
    cursor: default;
    display: block;
    width: 100%;
    padding: 0.375rem 2.25rem 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: $color-gray-dark;
    background-color: $color-white;
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill='none' stroke='%23343a40' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M2 5l6 6 6-6'/%3e%3c/svg%3e");
    background-repeat: no-repeat;
    background-position: right 0.75rem center;
    background-size: 16px 12px;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  }

  &__input {
    background-color: transparent;
    font-size: 1rem;
    padding: 0.25rem 1rem 0.25rem 0.25rem;
    margin-bottom: 0;
  }

  &__list--multiple {
    .choices__item,
    .choices__item.is-highlighted {
      background-color: $color-primary;
      border-color: $color-primary;
    }
  }
  &__list--single {
    padding: 0.25rem 1rem 0.625rem 0.25rem;
  }
  &[data-type*="select-multiple"] &__button,
  &[data-type*="text"] &__button {
    border-left: none;
    margin: 0;
  }
  &__list--dropdown &__item--selectable.is-highlighted,
  &__list[aria-expanded] &__item--selectable.is-highlighted {
    background-color: $color-gray-light;
  }
  &[data-type*="select-one"] &__inner {
    padding-bottom: 0;
  }

  &[data-type*="select-one"]::after {
    content: "";
    height: 0;
    width: 0;
    border-style: solid;
    border-color: #333 transparent transparent;
    border-width: 0;
    position: absolute;
    right: 11.5px;
    top: 50%;
    margin-top: -2.5px;
    pointer-events: none;
  }

  @media (min-width: 640px) {
    .choices__list--dropdown .choices__item--selectable,
    .choices__list[aria-expanded] .choices__item--selectable {
      padding-right: 0;
    }
  }
}

::-webkit-input-placeholder {
  color: rgba($color-gray-dark, 0.5);
}

/*---------------------------------------/*
 # COMPONENTS
/*---------------------------------------*/
.c-input {
  width: calc(50% - 0.25rem);

  &__field {
    height: 2.875rem;
    width: 100%;
  }
}
</style>
