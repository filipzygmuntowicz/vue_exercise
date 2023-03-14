<template>
    <nav
    :class="`navbar navbar-expand-lg navbar-${theme} bg-${theme}`">
        <div class="container-fluid">
            <!--<a class="navbar-brand" href="#">Stronka</a>-->
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <navbar-link
                v-for="(page, index) in publishedPages" :key="index"
                :page = "page"
                :index = "index"
            ></navbar-link>

            <li>
                <router-link 
                    active-class="active emphasize"
                    to="/pages"
                    class="nav-link"
                    aria-current="page"
                    >Pages
                </router-link>
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
            created() {
                this.getThemeSetting()
                this.pages = this.$pages.getAllPages()
                this.$bus.$on('page-updated', () => {
                    this.pages = [...this.$pages.getAllPages()]
                })
                this.$bus.$on('page-created', () => {
                    this.pages = [...this.$pages.getAllPages()]
                })
                this.$bus.$on('page-deleted', () => {
                    this.pages = [...this.$pages.getAllPages()]
                })
            },
            inject: ['$pages', '$bus'],
            computed: {
                publishedPages() {
                    return  this.pages.filter(p => p.published) 
                }
            },
            components: {
                NavbarLink
            },
            data() {
                return {
                    theme: 'light',
                    pages: []
                }
            },
            methods: {
                capitalize(string) {
                    return string[0].toUpperCase() + string.slice(1)
                },
                changeTheme() {
                    this.theme == 'light' ? this.theme = 'dark' : this.theme = 'light'
                    this.storeThemeSetting()
                },
                storeThemeSetting() {
                    localStorage.setItem('theme', this.theme)
                },
                getThemeSetting() {
                    let theme = localStorage.getItem('theme', this.theme)

                    if (theme) {
                        this.theme = theme
                    }
                }
            }
        }
</script>
<style scoped>
.emphasize {
    text-decoration: underline !important;
}
</style>