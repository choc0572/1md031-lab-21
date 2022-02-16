<template>
  <div class="burger" style="display: inline-block; ">
    <h2>{{burger.name}}</h2>
    <br />
    <img
      :src=burger.url
      alt="Span"
      title="Another in-line element"
      style="width: 200px"
    />
    <ul>
      <li>{{ burger.kCal }} kCal</li>
      <li>Gluten? <span id="ingredient" :v-if="burger.gluten">Yes</span></li>
      <li>Lactose? <span id="ingredient" :v-if="burger.lactose">Yes</span></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#ingredient {
  font-weight: 1000;
}

.burger {
  margin: 0 20px;
  padding: 10px;
}

.burgers {
  border: 10px double white;
  padding: 20px;
  color: #ffffff;
  background-color: black;
}
</style>
