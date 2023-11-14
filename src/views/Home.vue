<template>
  <div class="home">

    <p> Currently there are several clients to choose by, <br> choosing is done by writing client name<br> in the input
      below.</p>
    <small>Hint: Every letter, filters out unwanted names. <br><br></small>


    <input @keyup.enter="matchingNames" type="text" v-model="search">
    <div v-if="show">Currently corresponding values: </div>
    <div v-for="name in matchingNames" :key="name"> {{ name + "\n" }}</div>

  </div>
</template>

<script>

import { reactive, computed, ref } from 'vue'


export default {
  name: 'Home',
  methods: {
    data() {
      return {
        name: false
      }
    }

  },
  setup() {
    const search = ref("");
    const names = ref(['Stefan', 'Mario', 'Nikola', 'Aleksandar', 'Pavel','Simona', 'Marija','Velika','Andriana']);
    var show = ref(false);





    const matchingNames = (computed(() => {
      if (!search.value) {
        show.value = false;
        return names.value;
      }

      var calculate = names.value.map(element => element.toLowerCase()).filter((element) => {
        const lowSearch = search.value.toLowerCase();
        return element.includes(lowSearch);
      })
      //extra calculation needed so we can show first letter as Uppercase \/. 

      return calculate.map((word) => {
        const firstLetter = word.charAt(0).toUpperCase();
        const rest = word.slice(1);
        show.value = true;
        return firstLetter + rest;
      })
    }))


    return { names, search, matchingNames, show };
  }
}
</script>
