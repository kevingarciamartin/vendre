<script>
export default {
    name: "contact-list",
    data() {
        return {
            post: {}
        }
    },
    methods: {
        getPage(pageNumber) {
            if (pageNumber > 1) {
                const response = fetch("https://reqres.in/api/users?page=" + pageNumber)
                    .then(response => response.json())
                    .then(data => this.post = data)
            } else {
                const response = fetch("https://reqres.in/api/users")
                    .then(response => response.json())
                    .then(data => this.post = data)
            }
        }
    }, 
    mounted() {
        this.getPage()
    }
}
</script>

<template>
    <div class="list">
        <div class="card" v-for="person in post.data" :key="person.id">
            <img :src=person.avatar alt="Avatar">
            <div class="card-content">
                <p class="card-name">
                    {{ person.first_name }}
                    {{ person.last_name }}
                </p>
                <a :href=person.email class="card-email">Contact</a>
            </div>
        </div>
    </div>
    <div class="pagination">
        <button v-for="index in post.total_pages" :key="index.id" @click="getPage(index)">{{ index }}</button>
    </div>
</template>

<style>
.list {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: center;
    padding: 1rem;
}

.card {
    display: grid;
    justify-items: center;
    width: 10rem;
    aspect-ratio: 1 / 1;
    padding: 1rem;
    border-radius: 1rem;
    background: hsla(0, 0%, 0%, 0.05);
}

.card:hover {
    background: hsla(0, 0%, 0%, 0.1);
}

img {
    width: 70%;
    border-radius: 50%;
    aspect-ratio: 1;
    object-fit: cover;
} 

.card-content {
    display: grid;
    justify-items: center;
}

.card-name {
    font-weight: 900;
}

.card-email {
    text-decoration: none;
    color: steelblue;
}

.pagination {
    display: flex;
    justify-content: center;
    gap: 0.3em;
}

button {
    width: 2rem;
    aspect-ratio: 1;
    border-radius: 50%;
    border: none;
    cursor: pointer;
}

button:active,
button:focus-visible {
    background: lightblue;
}
</style>