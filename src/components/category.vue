<template>
  <div class="category">
    <div class="row">
      <div class="col-md-12" v-for="(category, index) in $store.state.categories" :key="index">
        <div v-if="cateId == category.categoryId">
          <h1>{{ title }} {{ category.categoryTitle }}</h1>
          <h5>{{ totalCount }}Counts <span>,</span> TotalAmount: {{ totalAmount }}$</h5>
        </div>
      </div>
    </div>
    <hr />
    <div class="row">
      <div class="col-md-4 col-lg-4" v-for="(data, index) in $store.state.products" :key="index">
        <h3 @click="goTodetail(data.productId)">{{ data.productTitle }}</h3>
        <img :src="data.image" class="img-fluid">
        <h4>{{ data.productPrice }}$</h4>
      </div>
    </div>
    <hr />
    <router-link class="nav-link" to="/">
      <button type="button" class="btn btn-primary">Return Home Page</button>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'category',
  data () {
    return {
      totalCount: 0,
      totalAmount: 0,
      cateId: this.$route.params.Cid,
      title: 'Category'
    }
  },
  methods: {
    goTodetail (prodId) {
      this.$router.push({ name: 'details', params: { Pid: prodId } })
    }
  },
  mounted: function () {
    this.$nextTick(function () {
      // do stuff with the DOM
      console.log('mounted', this.totalCount)
      this.totalCount = this.products.length
      this.products.forEach(product => {
        this.totalAmount += product.productPrice
      })
    })
  }
}
</script>
