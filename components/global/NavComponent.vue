<template>
    <div>
  <b-navbar fixed="top" toggleable="lg" type="light" variant="light">
    <nuxt-link class="navbar-brand" to="/">Home</nuxt-link>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav class="ml-auto">
        <nuxt-link class="nav-link" to="/">Home</nuxt-link>
        <nuxt-link class="nav-link" to="/about">About</nuxt-link>
        <nuxt-link class="nav-link" to="/blog">Blog</nuxt-link>
        <!-- <nuxt-link tag="button" :disabled="true" class="nav-link" to="/about">About</nuxt-link> -->
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav>
          <b-nav-item-dropdown text="Lang" right>
          <b-dropdown-item href="#">EN</b-dropdown-item>
          <b-dropdown-item href="#">ES</b-dropdown-item>
          <b-dropdown-item href="#">RU</b-dropdown-item>
          <b-dropdown-item href="#">FA</b-dropdown-item>
        </b-nav-item-dropdown>

        <b-nav-form>
            <div>
                <!-- <b-nav-item> -->
                    <b-button class="nav-item" style="background: transparent; border: 0" v-b-toggle.sidebar-right>
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="black" class="bi bi-search" viewBox="0 0 16 16">
                        <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
                    </svg>
                    </b-button>
                <!-- </b-nav-item> -->

                <b-sidebar id="sidebar-right" title="Sidebar" right shadow>
                    <template #default="{ hide }">
                <div class="px-3 py-2">
                    <p>Search Posts</p>
                    <search-input class=""></search-input>
                    <nav class="mb-3">
                    <b-nav vertical>
                        <b-nav-item active @click="hide">Active</b-nav-item>
                        <b-nav-item href="#link-1" @click="hide">Link</b-nav-item>
                        <b-nav-item href="#link-2" @click="hide">Another Link</b-nav-item>
                    </b-nav>
                </nav>
                <b-button variant="primary" block @click="hide">Close Sidebar</b-button>
                </div>
                </template>
                </b-sidebar>
            </div>
        </b-nav-form>

        
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</template>

<script>
export default {
    name: 'HeaderComponent',
}
</script>

<style>

button, 
button:focus,
.btn, 
.btn:focus,
.btn-secondary:focus, 
.btn-secondary.focus {
    outline: 0;
    box-shadow: none !important;
    }

</style>