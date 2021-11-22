<template>
 <div class="wrap">
   <h1 class="wrap__title">
     {{ title }}
   </h1>
 </div>
  
</template>

<script>

export default {
  name: 'headerApp',
  // props: ['title'],
  props: {
    title: {
      type: String,
      default: ''
    }
  },
  components: {
    
  }
}
</script>

<style scoped>
.wrap {
  text-align: center;
  width: 100%;
  padding: 25px 0;
  background-color: #640032;
  font-family: 'Roboto', sans-serif;
}
.wrap__title {
  font-size: 2rem;
  color: #FFF;
  font-weight: bold;
}
</style>
