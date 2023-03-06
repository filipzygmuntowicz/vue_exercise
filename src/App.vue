<template>
    <navbar
        :pages = "pages"
        :activePage = "activePage"
        :nav-link-click="(index) => activePage = index">
    </navbar>
    <page-viewer
        :page="pages[activePage]">
    </page-viewer>
</template>

<script>
import PageViewer from './components/PageViewer';
import Navbar from './components/Navbar';
export default {
    components: {
        PageViewer,
        Navbar
    },
    data() {
        return {
            activePage: 0,
            useDarkNavbar: false,
            theme: "light",
            pages: [
                {
                    link: {text: 'Home', url: 'index.html'},
                    pageTitle: 'Home Page',
                    content: 'This is the home content'
                },
                {
                    link: {text: 'About', url: 'about.html'},
                    pageTitle: 'About Page',
                    content: 'This is the about content'
                },
                {
                    link: {text: 'Contact', url: 'contact.html'},
                    pageTitle: 'Contact Page',
                    content: 'This is the contact content'
                }
            ]
            }
    }
}
</script>