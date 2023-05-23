<template>
    <navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index) => activePage=index"
    >

    </navbar>
      <page-viewer 
        :page="pages[activePage]">
    </page-viewer>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import Navbar from './components/Navbar.vue';
    export default {
        components: {
            PageViewer,
            Navbar
        },
        data() {
                return {
                    activePage: 0,
                    theme: "dark",
                    pages: [
                        {
                            link: {text: 'Home', url: 'home.html'},
                            pageTitle: 'Home Page',
                            content: 'This is home page'
                        },
                        {
                            link: {text: 'About', url: 'about.html'},
                            pageTitle: 'About Page',
                            content: 'This is About page'
                        },
                        {
                            link: {text: 'Contact', url: 'contact.html'},
                            pageTitle: 'Contact Page',
                            content: 'This is Contact page'
                        }
                    ]
                };
            }
    }
</script>