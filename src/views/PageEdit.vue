<template>
    <h4>Edit {{ page.pageTitle }}</h4>

    <div class="container mb-3">
        <form action="">
            <div class="mb-3">
                <label for="" class="form-label">
                    Page Title
                </label>
                <input
                    type="text"
                    class="form-control"
                    v-model="page.pageTitle"
                />
            </div>
            <div class="mb-3">
                <label for="" class="form-label">
                    Content
                </label>
                <textarea
                    type="text"
                    class="form-control"
                    rows="5"
                    v-model="page.content"
                ></textarea>
            </div>
            <div class="col">            
                <div class="mb-3">
                    <label for="" class="form-label">
                        Link Text
                    </label>
                    <input
                        type="text"
                        class="form-control"
                        v-model="page.link.text"
                    />
                </div>
                <div class="row mb-3">
                    <div class="form-check">
                        <input
                            class="form-check-input" 
                            type="checkbox"
                            v-model="page.published">
                        <label class="form-check-label" for="gridCheck1">
                            Published
                        </label>
                    </div>
                </div>
            </div>

            <div class="mb-3">
                <button
                    class="btn btn-primary"
                    @click.prevent="submit"
                >Edit</button>
                <button
                    class="btn btn-secondary"
                    @click.prevent="cancel"
                >Cancel</button>
                <button
                    class="btn btn-danger"
                    @click.prevent="deletePage"
                >Delete</button>
            </div>
        </form>
    </div>
</template>

<script setup>
import {inject} from 'vue'
import {useRouter} from 'vue-router'


const router = useRouter()
const pages = inject('$pages')
const {index} = defineProps(['index'])
const bus = inject('$bus')

let page = pages.getSinglePage(index)


function submit() {
    pages.editPage(index, page)
    bus.$emit('page-updated', {
        index,
        page
    })
    router.push({path: "/pages"})
}
function cancel() {
    router.push({path: "/pages"})
}
function deletePage() {
    pages.removePage(index)
    bus.$emit('page-deleted', {index})
    router.push({path: "/pages"})
}
</script>