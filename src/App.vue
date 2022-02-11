<template>
  <div id="app">
    <b-navbar class="justify-content-center" type="dark" variant="dark">
      <b-navbar-nav>
        <b-nav-item to="/"> Pricing</b-nav-item>
        <b-nav-item to="/details">Bitcoin details</b-nav-item>
        <b-nav-item to="/calculator">Bitcoin calculator</b-nav-item>
      </b-navbar-nav>
    </b-navbar>
    <router-view />
  </div>
</template>

<style>
.nav-bar-justify {
  justify-content: center;
}
</style>
