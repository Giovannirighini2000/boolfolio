<template>
    <template v-if="project">
        <div class="container">
            <h1>
                {{ project.title }}
            </h1>
            <p>
                {{ project.description ? project.description : 'non risulta nessuna descrizione del progetto creata' }}
            </p>
            <p>
                {{ project.date }}
            </p>
            <p>
                {{ project.url }}
            </p>


        </div>
    </template>
</template>
<script>
import axios from 'axios'
import ProjectCard from '../components/ProjectCard.vue';
export default (await import('vue')).defineComponent({
    components: {
        ProjectCard
    },
    data() {
        return {
            project: null
        }
    },
    props: [
        'slug'
    ],
    methods: {
        fetchProject() {
            axios.get(`http://127.0.0.1:8000/api/projects/${this.slug}`)
                .then(res => {
                    const { project } = res.data
                    this.project = project


                })
                .catch(err => {
                    console.log(err)

                })
        }

    },
    created() {
        this.fetchProject()
    },

    mounted() {
        // console.log(this.$route.params.slug)
        // altro methods
    }



})
</script>
<style></style>