<template>
  <header class="text-center bg-blue-800 text-white p-4 mb-10">
    <div class="text-3xl md:text-5xl font-bold mb-3"> 
      <i class="fa fa-viruses"></i>
      Covid-19 Tracker</div>
      <p>A webApp by Ayush</p>
    <p>
      API Provided by 
      <a class="text-blue-200" href="https://covid19api.com"
      target="_blank"
      >covid19api.com</a>
    </p>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  }
}
</script>
