<template>
    <h4>edit {{ page.pageTitle }}</h4>
    <form action="">
        <div class="mb-3">
            <label class="form-label" for="">Page Title
            </label>
            <input 
                class="form-control" 
                type="text"
                v-model="page.pageTitle"
                >
        </div>
        <div class="mb-3">
            <label class="form-label" for=""> Link Text
            </label>
            <input
                class="form-control" 
                type="text"
                v-model="page.linkText">
        </div>
        <div class="mb-3">
            <label class="form-label" for=""> Content
            </label>
            <textarea
                type="text"
                class="form-control"
                rows="5"
                v-model="page.content"
                >
            </textarea>
        </div>
        <div class="mb-3">
            <button 
            class="btn btn-primary"
            :disabled="isFormInvalid"
            @click.prevent="submit">
                Submit
            </button>
        </div>
        <div class="mb-3">
            <button 
            class="btn btn-primary"
            :disabled="isFormInvalid"
            @click.prevent="">
                Cancel
            </button>
        </div>
        <div class="row mb-3">
            <div class="form-check">
                <input class="form-check-input" type="checkbox" v-model="page.published">
                <label class="form-check-input" for="gridCheck1">Published</label>
            </div>
        </div>
    </form>
</template>
<script setup>
import { inject } from 'vue';
import { useRoute } from 'vue-router';
const route= useRoute();
const pages = inject('$pages');
const {index} = defineProps([ 'index']);
const bus = inject('$bus');
let page = pages.getSinglePage(index);

function submit() {
    pages.editPage(index, page);

    bus.$emit('page-updated', {
        index,
        page 
    });
}
</script>
