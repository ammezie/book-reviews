<template>
  <section class="section">
    <div class="container">
        <h1 class="title has-text-centered">Books</h1>
        <div class="columns is-multiline">
            <book
                v-for="book in books"
                :key="book.id"
                :book="book">
            </book>
        </div>
    </div>
</section>
</template>

<script>
  import Book from './Book.vue'
  import axios from 'axios'

  export default {
    name: 'BookList',

    components: {
      Book
    },

    data () {
      return {
        books: []
      }
    },

    created () {
      this.fetchBooks()
    },

    methods: {
      fetchBooks () {
        axios.get('https://book-reviews-api.herokuapp.com/api/books').then(response => {
          this.books = response.data.data
        }).catch(error => {
          console.log(error)
        })
      }
    }
  }
</script>
