<template>
  <div>
    <div class="header">
      <input type="text" v-model="searchItem" placeholder="Search books" class="search-box" />
      <div style="display: flex; gap: 15px;">
        <p style="padding-top: 10%;">{{ booksData.length }} books</p>
        <div>
          <p>Sort by</p>
          <select name="sort" id="sort" class="dropdown" v-model="sortValue">
            <option value="T-Asc">Title: A to Z</option>
            <option value="T-Dec">Title: Z to A</option>
            <option value="A-Asc">Author: A to Z</option>
            <option value="A-Dec">Author: Z to A</option>
            <option value="Y-Asc">Year: Old to New</option>
            <option value="Y-Dec">Year: New to Old</option>
          </select>
        </div>
      </div>

    </div>
    <p v-if="booksData.length === 0" > {{ message }}</p>
    <div class="container">
      <CardComponent v-for="book in booksData" :key="book.title" :book="book" />
    </div>
  </div>
</template>

<script>
import books from "../data/books.json"
import CardComponent from './CardComponent.vue';
export default {
  name: 'HelloWorld',
  components: {
    CardComponent
  },
  data() {
    return {
      booksData: books,
      searchItem: '',
      sortValue: 'T-A-Z',
      message: 'No books found'
    }
  },
  watch: {
    searchItem(newValue) {
      if(newValue === '') return this.booksData = books;

      const filteredData = books.filter((data) => {
        return (data.title.toLowerCase().startsWith(newValue.toLowerCase()));
      })
      this.booksData = filteredData
    },

    sortValue(newValue) {
      if (newValue.includes('Asc')) {
        if (newValue === 'T-Asc') {
          const sortedData = books.sort((a, b) => {
            let t1 = a.title.toLowerCase();
            let t2 = b.title.toLowerCase();

            return (t1 > t2) ? 1 : (t1 < t2) ? -1 : 0;
          })
          this.booksData = sortedData;
        } else if (newValue === 'A-Asc') {
          const sortedData = books.sort((a, b) => {
            let t1 = a.author.toLowerCase();
            let t2 = b.author.toLowerCase();

            return (t1 > t2) ? 1 : (t1 < t2) ? -1 : 0;
          })
          this.booksData = sortedData;
        } else {
          const sortedData = books.sort((a, b) => {
            return (a.year > b.year) ? 1 : (a.year < b.year) ? -1 : 0;
          })
          this.booksData = sortedData;
        }
      } else {
        if (newValue === 'T-Dec') {
          console.log('inside t-Dec');
          const sortedData = books.sort((a, b) => {
            let t1 = a.title.toLowerCase();
            let t2 = b.title.toLowerCase();

            return (t1 < t2) ? 1 : (t1 > t2) ? -1 : 0;
          })
          this.booksData = sortedData;
        } else if (newValue === 'A-Dec') {
          const sortedData = books.sort((a, b) => {
            let t1 = a.author.toLowerCase();
            let t2 = b.author.toLowerCase();

            return (t1 < t2) ? 1 : (t1 > t2) ? -1 : 0;
          })
          this.booksData = sortedData;
        } else {
          const sortedData = books.sort((a, b) => {
            return (a.year < b.year) ? 1 : (a.year > b.year) ? -1 : 0;

          })
          this.booksData = sortedData;
        }
      }
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search-box {
  margin-left: 12%;
  border-bottom: 2px solid grey;
  width: 150px;
}

.dropdown {
  border-bottom: 1px solid black;
  padding-top: 2%;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.container {
  display: flex;
  gap: 2%;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: center;
  margin-top: 5%;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
