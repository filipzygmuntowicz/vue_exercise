<template>
    <nav
    :class="`navbar navbar-expand-lg navbar-${theme} bg-${theme}`">
        <div class="container-fluid">
            <!--<a class="navbar-brand" href="#">Stronka</a>-->
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li v-for="(page, index) in pages" :key="index">
                    <navbar-link
                        :page = "page"
                        :isActive = "activePage === index"
                        @click.prevent="navLinkClick(index)"
                    ></navbar-link>
                </li>
            </ul>
            <form class="d-flex">
                <button 
                    class="btn btn-primary"
                    @click.prevent="changeTheme()">
                    {{ theme == 'light' ? 'Dark mode' : 'Light mode' }}
                </button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue'
    export default {
            components: {
                NavbarLink
            },
            props: ['pages', 'activePage', 'navLinkClick'],
            data() {
                return {
                    theme: 'light',
                    activePage: 0
                }
            },
            methods: {
                capitalize(string) {
                    return string[0].toUpperCase() + string.slice(1)
                },
                changeTheme() {
                    this.theme == 'light' ? this.theme = 'dark' : this.theme = 'light'
                }
            }
        }
</script>