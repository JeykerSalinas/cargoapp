<template>
  <div class="container">
    <table class="table table-dark table-striped">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Name</th>
          <th scope="col">Country</th>
          <th scope="col">Continent</th>
          <th scope="col">Coordinates</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="d in data" v-bind:key="d.id">
          <td>{{ d.id }}</td>
          <td>{{ d.name }}</td>
          <td>{{ d.country }}</td>
          <td>{{ d.continent }}</td>
          <td>{{ d.coordinates }}</td>
        </tr>
      </tbody>
    </table>
    <VueTailwindPagination
      
      :current="currentPage"
      :total="total"
      :per-page="perPage"
      :classes ="classObj"
      @page-changed="onPageClick($event)"
    />
  </div>
</template>

<script>
import axios from "axios";
import VueTailwindPagination from "@ocrv/vue-tailwind-pagination";
import '@ocrv/vue-tailwind-pagination/styles'

export default {
  components:{
    VueTailwindPagination,
  },
  data() {
    return {
      currentPage: 0,
      perPage: 0,
      total: 0,
      data: [],
      classObject:{
        button: 'color: green'
      }
    };
  },
  methods: {
    onPageClick(event) {
      console.log(event)
      this.currentPage = event;
      this.getData(this.currentPage);
    },
   async getData (pageNumber){
     axios.get(`http://apitest.cargofive.com/api/ports?page=${pageNumber}`).then((response) => {
      const responseData = response.data;
      this.currentPage = responseData.meta.current_page;
      this.perPage = responseData.meta.per_page;
      this.total = responseData.meta.total;
      this.data = responseData.data;
    });

   }

  },
  mounted() {
    this.getData()
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
