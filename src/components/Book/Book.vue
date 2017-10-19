<template>
  <div class="column is-one-third">
    <div class="card">
      <header class="card-header">
        <h2 class="card-header-title">
          {{ book.title }}
        </h2>
      </header>
      <div class="card-content">
        <div class="content">
          <p>{{ book.description }}</p>

          <p>
            Average rating: <strong>{{ book.average_rating }}</strong>
          </p>

          <div class="field">
            <label class="label">Rate this</label>
            <div class="control">
              <div class="select" @change="rateBook(book.id, $event)">
                <select>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                  <option value="5">5</option>
                </select>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Book',

    props: ['book'],

    data () {
      return {

      }
    },

    methods: {
      rateBook (bookId, event) {
        axios.post('https://book-reviews-api.herokuapp.com/api/ratings', {
          book_id: bookId,
          rating: event.target.value
        })
        .then(response => {
          return 'Success'
        }).catch(error => {
          console.log(error)
        })
      }
    }
  }
</script>
