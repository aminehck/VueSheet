<template>
  <div id="app">
    <div id="nav">
      <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
        <router-link class="navbar-brand col-sm-3 col-md-2 mr-0" to="/">VueSheet</router-link>
        <!-- <input class="form-control form-control-dark w-100" type="text" placeholder="Search" aria-label="Search"> -->
        <ul class="navbar-nav px-3">
          <li class="nav-item text-nowrap">
            <router-link class="nav-link" to="/add">+ Add New Row</router-link>
          </li>
        </ul>
      </nav>
    </div>
    <router-view/>
  </div>
</template>

<style>

</style>
