<template>
    <navbar>
    </navbar>
    
    <router-view></router-view>

    <!-- <div v-show="false">hide this content with css</div>
    <page-viewer
        v-if="pages.length > 0"
        :page="publishedPages[activePage]">
    </page-viewer> 
    <create-page
        @page-created="pageCreated">
    </create-page> -->

</template>

<script>
import Navbar from './components/Navbar';

export default {
    components: {
        Navbar
    },
    methods: {
        pageCreated(pageObj) {
            this.pages.push(pageObj)
        }
    }
}
</script>
