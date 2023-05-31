<template>
    <navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index) => activePage=index"
    >

    </navbar>
      <page-viewer
        :page="publishedPages[activePage]">
    </page-viewer>
    <create-page
    :page-created="pageCreated">

    </create-page>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import CreatePage from './components/CreatePage.vue';
import Navbar from './components/Navbar.vue';
    export default {
        components: {
            PageViewer,
            Navbar,
            CreatePage
        },
        created() {
            this.getPages()
        },
    computed: {
        publishedPages() {
            return this.pages.filter(p => p.published);
        }
    },
        data() {
                return {
                    activePage: 0,
                    theme: "dark",
                    pages: []
                };
            },
            methods: {
                async getPages() {
                    let res = await fetch('pages.json')
                    let data = await res.json();
                    this.pages = data;
                },
                pageCreated(pageTitle) {
                    this.pages.push(pageTitle)
                }
            }
    }
</script>