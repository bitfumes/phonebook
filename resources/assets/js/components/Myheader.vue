<template>
	<nav class="navbar" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a class="navbar-item" href="http://bulma.io">
      <img src="" alt="Bitfumes" width="112" height="28">
    </a>

    <div class="navbar-menu is-active">
      <router-link to="/home" class="navbar-item">Home</router-link>
      <router-link to="/about" class="navbar-item">About</router-link>
    </div>

    <button class="button navbar-burger">
      <span></span>
      <span></span>
      <span></span>
    </button>
  </div>
</nav>
</template>