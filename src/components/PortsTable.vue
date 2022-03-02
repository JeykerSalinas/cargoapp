<template>
  <div class="hello">
    <h1>{{ data }}</h1>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      currentPage: 0,
      perPage: 0,
      total: 0,
      data: [],
    }
  },
  mounted () {
    axios
      .get('http://apitest.cargofive.com/api/ports')
      .then(response =>{ 
       const responseData = response.data;
      this.currentPage = responseData.meta.current_page;
      this.perPage = responseData.meta.per_page;
      this.total = responseData.meta.total;
      this.data = responseData.data;}

        )
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
