<template>
  <div class="v-table">
    <div class="v-table__header">
      <p @click="sortByFName">First name
        <i class="material-icons ml-3">sort</i>
      </p>
      <p @click="sortByLName">Last name
        <i class="material-icons ml-3">sort</i>
      </p>
      <p @click="sortById">Id
        <i class="material-icons ml-3">sort</i>
      </p>
      <p>Email
        <i class="material-icons ml-3">sort</i>
      </p>
    </div>
    <div class="v-table__body">
      <v-table-row 
        v-for="row in paginationUsers"
        :key="row.id"
        :row__data="row"
      />
    </div>
    <div class="v-table__pagination">
      <div class="page" 
        v-for="page in pages"
        :key="page"
        :class="{ 'page__selected':page === pageNumber }"
        @click="pageClick(page)"
          >{{ page }}</div>
    </div>
    
  </div>
</template>

<script>
import vTableRow from '../table/v-table-row'


export default {
  name: 'v-table',
  components: {
    vTableRow
  },
  props: {
    users_data: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data() {
    return {
      usersPerPage: 5,
      pageNumber: 1
    }
  },
  computed: {
    pages() {
      return Math.ceil(this.users_data.length / 5)
    },
    paginationUsers() {
      let from = (this.pageNumber - 1) * this.usersPerPage;
      let to = from + this.usersPerPage;
      return this.users_data.slice(from, to);
    }
  },
  methods: {
    pageClick(page) {
      this.pageNumber = page
    },
    sortByFName() {
      this.users_data.sort((a, b) => a.first_name.localeCompare(b.first_name))
    },
    sortByLName() {
      this.users_data.sort((a, b) => a.last_name.localeCompare(b.last_name))
    },
    sortById() {
      this.users_data.sort((a, b) => a.id - b.id)
    }
  }
}
</script>

<style>

  .table__body {
    text-align: start;
  }
  .ml-3 {
    margin-left: 3px;
  }
  .v-table {
    max-width: 900px;
    margin: 0 auto;
    background: #d0d0d0;
    padding: 20px;
    border-radius: 12px;
  }
  .v-table__header {
    display: flex;
    justify-content: space-around;
    border-bottom: solid 1px rgb(94, 169, 255);
  }
  .v-table__header p {
    flex-basis: 25%;
    text-align: left;
    display: flex;
    align-items: center;
    cursor: pointer;
  }
  .v-table__pagination {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 30px;
  }
  .page {
    padding: 8px 13px;
    border: solid 1px rgb(94, 169, 255);
    margin-right: 10px;
    border-radius: 8px;
  }
  .page:hover {
    background: rgba(73, 77, 73, 0.2);
    cursor: pointer;
  }
  .page__selected {
    background: #434343;
    cursor: pointer;
    color: aliceblue;
  }
</style>