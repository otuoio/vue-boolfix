<template>
    <main>
        <div>
            <ul v-for="(movie, index) in movieFind"
                :key="index">
                <li>
                    {{ movie.title || movie.name}}
                </li>
                <li>
                    {{ movie.original_title || movie.original_name }}
                </li>
                <li>
                    <country-flag :country='getFlags(movie.original_language)' size='small' shadow />
                </li>
                <li>
                    {{ movie.vote_average}}
                </li>
            </ul>
        </div>
    </main>
</template>

<script>

export default {
    name: "Main",
    data() {
        return {

        }
    },
    props: {
        movieFind: {
            type: Array,
        }
    },
    created() {
        
    },
    computed: {
        
    },
    methods: {
        getFlags(lan) {
            if (lan === 'en') {
                return 'gb';
            } else if (lan === 'ja') {
                return 'jp';
            } else {
                return lan;
            };
        }
    }
}
</script>

<style>

</style>