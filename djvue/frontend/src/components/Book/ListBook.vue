<template lang="html">
  <div class="container">
    <div class="row">
      <div class="col text-left">
        <h2>Listado de libros</h2>
        <div>
          <b-button size="sm"  variant="info" :to="{ name:'NewBook' }">Añadir Libro</b-button>
        </div>
	      </br>
        <div class="col-md-12">
          <b-table striped hover :items="books" :fields="fields">
            <template v-slot:cell(action)="row">
              <b-button type="submit" size="sm" variant="primary"  :to="{ name:'EditBook', params: {bookId: row.item.id} }">Editar</b-button>
              <b-button type="submit" size="sm" variant="danger" :to="{ name:'DeleteBook', params: {bookId: row.item.id} }">Eliminar</b-button>
            </template>
          </b-table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      fields: [
        { key: 'title', label: 'Título' },
        { key: 'description', label: 'Descripción' },
        { key: 'action', label: '' }
      ],
      books: []
    }
  },
  methods: {
    getBooks () {
      const path = 'http://localhost:8000/api/v1.0/books/'
      axios.get(path).then((response) => {
        this.books = response.data
      })
      .catch((error) => {
        console.log(error)
      })
    }
  },
  created(){
    this.getBooks()
  }
}
</script>

<style lang="css" scoped>
</style>
