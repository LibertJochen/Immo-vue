<template>
  <!-- ======= Header/Navbar ======= -->
  <nav class="navbar navbar-default navbar-trans navbar-expand-lg fixed-top">
    <div class="container">
      <button class="navbar-toggler collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#navbarDefault" aria-controls="navbarDefault" aria-expanded="false" aria-label="Toggle navigation">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <a class="navbar-brand c-brand" href="#">WDD<span class="u-color-secondary">Immo</span></a>

      <div class="navbar-collapse collapse justify-content-center" id="navbarDefault">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link active" href="#">Home</a>
          </li>

          <li class="nav-item">
            <a class="nav-link" href="#">Over ons</a>
          </li>

          <li class="nav-item">
            <a class="nav-link" href="index.html">Te koop</a>
          </li>

          <li class="nav-item">
            <a class="nav-link" href="#">Nieuws</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Kaart</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Contact</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <!-- End Header/Navbar -->
</template>

<script></script>

<style lang="scss">
/*---------------------------------------/*
 # SETTINGS
/*---------------------------------------*/
$color-primary: #2eca6a;
$color-white: #fff;
$color-black: #000;

/*---------------------------------------/*
 # GENERIC - BOOTSTRAP
/*---------------------------------------*/
.navbar-default {
  transition: all 0.5s ease-in-out;
  background-color: $color-white;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  box-shadow: 1px 2px 0.75rem rgba(100, 100, 100, 0.3);

  .nav-search {
    color: $color-black;
    font-size: 1.5rem;
  }

  &.navbar-reduce {
    box-shadow: 1px 2px 0.75rem rgba(100, 100, 100, 0.3);
  }

  &.navbar-trans .nav-item,
  &.navbar-reduce .nav-item {
    position: relative;
    padding-right: 10px;
    padding-bottom: 8px;
    margin-left: 0;
  }

  @media (min-width: 768px) {
    &.navbar-trans .nav-item,
    &.navbar-reduce .nav-item {
      margin-left: 15px;
    }
  }
  &.navbar-trans .nav-link,
  &.navbar-reduce .nav-link {
    font-size: 1.1rem;
    color: $color-black;
    font-weight: 600;
    letter-spacing: 0.03em;
    transition: all 0.1s ease-in-out;
    position: relative;
    padding-left: 0;
    padding-right: 0;
    display: inline-block;
  }
  &.navbar-trans .nav-link:before,
  &.navbar-reduce .nav-link:before {
    content: "";
    position: absolute;
    bottom: 5px;
    left: 0;
    width: 100%;
    height: 2px;
    z-index: 0;
    background-color: $color-primary;
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 0.2s ease-out, opacity 0.2s ease-out 0.3s;
  }
  &.navbar-trans .nav-link:hover,
  &.navbar-reduce .nav-link:hover {
    color: $color-black;
  }
  &.navbar-trans .nav-link:hover:before,
  &.navbar-reduce .nav-link:hover:before {
    transform: scaleX(1);
    transform-origin: left;
  }
  &.navbar-trans .show > .nav-link:before,
  &.navbar-trans .active > .nav-link:before,
  &.navbar-trans .nav-link.show:before,
  &.navbar-trans .nav-link.active:before,
  &.navbar-reduce .show > .nav-link:before,
  &.navbar-reduce .active > .nav-link:before,
  &.navbar-reduce .nav-link.show:before,
  &.navbar-reduce .nav-link.active:before {
    transform: scaleX(1);
  }
  &.navbar-trans .nav-link:before {
    background-color: $color-primary;
  }
  &.navbar-trans .nav-link:hover {
    color: $color-black;
  }
  &.navbar-trans .show > .nav-link,
  &.navbar-trans .active > .nav-link,
  &.navbar-trans .nav-link.show,
  &.navbar-trans .nav-link.active {
    color: $color-black;
  }
  &.navbar-reduce {
    transition: all 0.5s ease-in-out;
    padding-top: 19px;
    padding-bottom: 19px;

    .nav-link {
      color: $color-black;
      &:before {
        background-color: $color-primary;
      }
      &:hover {
        color: $color-black;
      }
    }

    .show > .nav-link,
    .active > .nav-link,
    .nav-link.show,
    .nav-link.active {
      color: $color-black;
    }
    .navbar-brand {
      color: $color-black;
    }
  }
  .dropdown {
    .dropdown-menu {
      border-top: 0;
      border-left: 4px solid $color-primary;
      border-right: 0;
      border-bottom: 0;
      transform: translate3d(0px, 40px, 0px);
      opacity: 0;
      filter: alpha(opacity=0);
      visibility: hidden;
      transition: all 0.5s cubic-bezier(0.3, 0.65, 0.355, 1) 0s, opacity 0.31s ease 0s, height 0s linear 0.36s;
      margin: 0;
      border-radius: 0;
      padding: 12px 0;

      @media (min-width: 768px) {
        border-top: 4px solid $color-primary;
        border-left: 0;
        display: block;
        position: absolute;
        box-shadow: 0 2px rgba(17, 16, 15, 0.1), 0 2px 10px rgba(20, 19, 18, 0.1);
      }
      .dropdown-item {
        padding: 12px 18px;
        transition: all 500ms ease;
        font-weight: 600;
        min-width: 220px;

        &:hover {
          background-color: $color-white;
          color: $color-primary;
          transition: all 500ms ease;
        }
        &.active {
          background-color: $color-white;
          color: $color-primary;
        }
      }
    }
    &:hover {
      .dropdown-menu {
        transform: translate3d(0px, 0px, 0px);
        visibility: visible;
        opacity: 1;
        filter: alpha(opacity=1);
      }
    }
  }
}

/*------/ Hamburger Navbar /------*/
.navbar-toggler {
  position: relative;

  &:focus,
  &:active {
    outline: 0;
  }

  span {
    display: block;
    background-color: $color-black;
    height: 3px;
    width: 25px;
    margin-top: 4px;
    margin-bottom: 4px;
    transform: rotate(0deg);
    left: 0;
    opacity: 1;

    &:nth-child(1),
    &:nth-child(3) {
      transition: transform 0.35s ease-in-out;
    }
  }
  &:not(.collapsed) {
    span {
      &:nth-child(1) {
        position: absolute;
        left: 12px;
        top: 10px;
        transform: rotate(135deg);
        opacity: 0.9;
      }
      &:nth-child(2) {
        height: 12px;
        visibility: hidden;
        background-color: transparent;
      }
      &:nth-child(3) {
        position: absolute;
        left: 12px;
        top: 10px;
        transform: rotate(-135deg);
        opacity: 0.9;
      }
    }
  }
}

/*---------------------------------------/*
 # COMPONENTS
/*---------------------------------------*/
.c-brand {
  color: $color-black;
  font-size: 2rem;
  font-weight: 600;

  &:hover span {
    color: $color-black;
  }

  @media (max-width: 767px) {
    font-size: 1.8rem;
  }
}
</style>
