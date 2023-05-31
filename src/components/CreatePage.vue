<template>
    <div class="container mb-3">
        <form action="">
            <div class="mb-3">
                <label class="form-label" for="">Page Title
                </label>
                <input 
                    class="form-control" 
                    type="text"
                    v-model="pageTitle"
                    >
            </div>
            <div class="mb-3">
                <label class="form-label" for=""> Link Text
                </label>
                <input
                    class="form-control" 
                    type="text"
                    v-model="linkText">
            </div>
            <div class="mb-3">
                <label class="form-label" for="">Link URL
                </label>
                <input 
                    class="form-control" 
                    type="text"
                    v-model="linkURL"
                    >
            </div>
            <div class="mb-3">
                <label class="form-label" for=""> Content
                </label>
                <textarea
                    type="text"
                    class="form-control"
                    rows="5"
                    v-model="content"
                    >
                </textarea>
            </div>
            <div class="mb-3">
                <button 
                class="btn btn-primary"
                :disabled="isFormInvalid"
                @click.prevent="submitForm">
                    Create Page
                </button>
            </div>
            <div class="row mb-3">
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" v-model="published">
                    <label class="form-check-input" for="gridCheck1">Published</label>
                </div>
            </div>
        </form>
    </div>
</template>
<script>
export default {
    props: ['pageCreated'],
    computed: {
        isFormInvalid() {
            return !this.pageTitle || !this.content || !this.linkText || !this.linkURL;
        }
    },
    data() {
        return {
            pageTitle: '',
            content: '',
            linkText: '',
            linkURL: '',
            published: true
        }
    },
    methods: {
        submitForm() {
            if(!this.pageTitle || !this.content || !this.linkText || !this.linkURL) {
                alert("Please fill the form");
                return;
            }

            this.pageCreated({
                pageTitle: this.pageTitle,
                content: this.content,
                link: {
                    text: this.linkText,
                    url: this.linkURL
                },
                published: this.published 
            })

            this.pageTitle= '',
            this.content = '',
            this.linkText= '',
            this.linkURL= '',
            this.published= true
        }
    },
    watch: {
        pageTitle(newTitle, oldTitle) {
            if(this.linkText === oldTitle) {
                this.linkText = newTitle;
            }
        }
    }
}
</script>