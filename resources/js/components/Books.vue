
 // Todo: Create Books component @citical
 // Todo: create search functinoality @critical
 // Todo: Create migrations to store favorite books @critical
 // Todo: create draggable list of books @critical


<template>
    <div>
       <h1>Books</h1>
        <categories></categories>
       <!-- <input type="text" id="search" v-model="search"><br>
       <button type="submit" @click="booksList($event)">Get Books</button> -->
    </div>
</template>

<script>
    export default {

        data() {
            return {
                books: [],
                book: {
                    id: '',
                    title: '',
                    body: ''
                },
                names: []
            }
        },
        methods: {
            fetchBooks(type) {
                const apiKey = 'DiP60FYqGbxKfMZBBIPhwBSPhUWA2EkL';
                const booksUrl = `https://api.nytimes.com/svc/books/v3/lists.json?list-name=${type}&api-key=${apiKey}`;
                console.log(booksUrl)
                fetch(booksUrl, { method: 'get' })
                    .then(res => res.json())
                    .then(res => {
                        this.books = res.results
                    })
                    .catch(error => {
                        console.log(error)
                    })
            },
            booksList(event) {
                event.preventDefault()
                console.log(this.search)
                // console.log(this.fetchBooks(this.search))
            },

        }
    }
</script>
