<template>
  <div class="col-md-4" v-for="house in houses">
    <div class="c-pand">
      <div class="c-pand__img">
        <img :src="house.photos[0]" alt="" class="c-pand__img img-fluid" />
      </div>
      <div class="c-pand__overlay">
        <div class="c-pand__content">
          <div class="c-pand__header">
            <h2 class="c-pand__title">{{ house.name }}</h2>
            {{ house.address }}, {{ house.city }}, {{ house.country }}
          </div>
          <div class="c-pand__body">
            <div class="pb-1 d-flex">
              <span class="c-pand__price">&euro; {{ house.price.toLocaleString() }}</span>
            </div>
          </div>
          <div class="c-pand__footer">
            <ul class="c-pand__info d-flex justify-content-around">
              <li>
                <h4 class="c-pand__label">Type</h4>
                <span>{{ house.type.description }}</span>
              </li>
              <li>
                <h4 class="c-pand__label">Slpks</h4>
                <span>{{ house.bedrooms }}</span>
              </li>
              <li>
                <h4 class="c-pand__label">Badk</h4>
                <span>{{ house.bathrooms }}</span>
              </li>
              <li>
                <h4 class="c-pand__label">Garage</h4>
                <span>{{ house.garage ? "Ja" : "Nee" }}</span>
              </li>
            </ul>
          </div>
          <div class="c-pand__footer">
            <h4>Amenities</h4>
            <ul>
              <li v-for="amenity in house.amenities" :key="amenity">{{ amenity }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//1 Import de nodige items
import { ref } from "vue";
//2 Export
export default {
  //2.2 Props
  props: {
    houses: { type: Array, required: true },
  },
};
</script>

<style lang="scss">
/*---------------------------------------/*
 # SETTINGS
/*---------------------------------------*/
$color-white: #fff;
$color-primary: #2eca6a;
$color-gray-dark: #313131;

/*---------------------------------------/*
 # COMPONENTS
/*---------------------------------------*/
.c-pand {
  position: relative;
  overflow: hidden;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;

  @media (max-width: 767px) {
    margin-bottom: 2.5rem;
  }

  @media (min-width: 768px) {
    margin-bottom: 2.5rem;
  }

  span {
    line-height: 0;
  }

  &__img {
    transition: 0.8s all ease-in-out;
    aspect-ratio: 3 / 2;
  }

  &__overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
  }

  &__content {
    transition: all 0.5s ease-in;
    position: absolute;
    width: 100%;
    bottom: 0px;
    // z-index: 2;

    @media (min-width: 768px) {
      bottom: -20px;
    }

    @media (min-width: 992px) {
      bottom: 0px;
    }
  }

  &__header {
    padding: 0 1rem;
    color: $color-white;
    margin-bottom: 0.5rem;
    text-shadow: 0 0 4px rgba(0, 0, 0, 0.7);
  }
  &__title {
    color: $color-white;
    margin-bottom: 0;
    padding-bottom: 0;
    font-size: 1.3rem;
  }

  &__body {
    z-index: 2;
    transition: all 0.5s ease-in;
    padding: 0rem 1rem 2rem 1rem;
    .price-box {
      padding-bottom: 0.5rem;
    }
  }

  &__price {
    color: $color-white;
    padding: 0.7rem 0.8rem 0.6rem 0.8rem;
    border: 2px solid rgb(46, 202, 106);
    border-radius: 50px;
    text-transform: uppercase;
    letter-spacing: 0.03em;
    background-color: rgba(46, 202, 106, 0.6);

    @media (min-width: 768px) {
      font-size: 0.9rem;
    }
    @media (min-width: 992px) {
      font-size: 1rem;
    }
  }

  &__footer {
    width: 100%;
    position: absolute;
    z-index: 2;
    background-color: $color-primary;
  }

  &__info {
    list-style: none;
    margin-bottom: 0;
    padding: 0.5rem 0;
    li span {
      color: $color-white;
      font-size: 0.9rem;
    }
  }

  &__label {
    font-size: 1rem;
    color: $color-gray-dark;

    @media (min-width: 768px) {
      font-size: 0.9rem;
    }
    @media (min-width: 992px) {
      font-size: 1rem;
    }
  }

  &:hover {
    @media (min-width: 768px) {
      .c-pand__img {
        transform: scale(1.2);
      }

      .c-pand__content {
        bottom: 60px;
      }

      .c-pand__content {
        bottom: 60px;
      }
      .c-pand__body {
        padding-bottom: 1rem;
      }
    }
    @media (min-width: 992px) {
      .c-pand__content {
        bottom: 64px;
      }
    }
  }

  @media (max-width: 767px) {
    &__content {
      bottom: 65px;
    }
    &__body {
      padding-bottom: 1rem;
    }
  }
}
</style>
