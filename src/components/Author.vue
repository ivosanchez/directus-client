<template>
  <p class="author">{{ name }}</p>
</template>

<script>
import axios from 'axios';
import { API } from '@/constants';
export default {
    name: 'Author',
    props: ['author'],
    data() {
        return {
            name: ''
        };
    },
    methods: {
        async getAuthor() {
            if (localStorage.getItem(`eightray_author_${this.author}`) === null) {
                let response = await axios.get(`${API.user}${this.author}`);
                this.name = `${response.data.data.first_name} ${response.data.data.last_name}`;
                localStorage.setItem(`eightray_author_${this.author}`, this.name);
            } else {
                this.name = localStorage.getItem(`eightray_author_${this.author}`);
            }
        }
    },
    beforeMount() {
        this.getAuthor();
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
p {
  text-align: center;
}
</style>
