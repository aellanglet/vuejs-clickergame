<template>
  <div class="score">
    <table style="width:100%">
      <tr>
        <th>User</th>
        <th>Level</th>
        <th>Food</th>
        <th>Wood</th>
        <th>Gold</th>
      </tr>
      <br>
      <tr>
        <th>{{ user.name }}</th>
        <th>{{ user.level }}</th>
        <th>{{ resources.food }}</th>
        <th>{{ resources.wood }}</th>
        <th>{{ resources.gold }}</th>
      </tr>
      <br>
      <tr>
        <th></th>
        <th></th>
        <th><button v-on:click="incrementFood">+1</button></th>
        <th><button v-on:click="incrementWood">+1</button></th>
        <th><button v-on:click="incrementGold">+1</button></th>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "score",
  props: {
    resources: {
      type: Object,
      required: true
    },
    user: {
      type: Object,
      required: true
    },
    maxLevel: {
      type: Number,
      required: true
    }
  },
  /*  data() {
    return {
      msg: "Is this a VueJS Clicker game ?"
    };
  }
  */
  methods: {
    incrementFood() {
      this.resources.food++;
    },
    incrementWood() {
      this.resources.wood++;
    },
    incrementGold() {
      this.resources.gold++;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
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
