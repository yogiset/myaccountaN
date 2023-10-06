<template>
    <nav class="navbar is-light">
    <div class="container">
    <div class="navbar-brand">
    <button class="button navbar-burger">
    <span></span>
    <span></span>
    <span></span>
    </button>
    </div>
    <div class="navbar-menu">
    <div class="navbar-end">
    <template>
    <nuxt-link class="navbar-item" to="/karyawan">Karyawan</nuxt-link>
    <nuxt-link class="navbar-item" to="/barang">Barang</nuxt-link>
    <div class="navbar-item has-dropdown is-hoverable">
    <a class="navbar-link">
    My Account
    </a>
    <div class="navbar-dropdown">
    <nuxt-link class="navbar-item" to="/profile">My Profile</nuxt-link>
    <hr class="navbar-divider"/>
    <a class="navbar-item" @click="logout">Logout</a>
    </div>
    </div>
    </template>
    </div>
    </div>
    </div>
    </nav>
</template>

<script>

export default {
computed: {

    },

methods: {
async logout() {

        },
    },


}
</script>