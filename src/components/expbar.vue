<template>
  <div>
    <div class="expbar">
      <div id="expbar" v-bind:style="{width: getXpPercent(user.exp,user.level) + '%'}">{{ (user.level === this.maxLevel) ? getXpForNextLevel(user.level) : user.exp + " / " + getXpForNextLevel(user.level) }}</div>
    </div>
    <h2>{{ (user.level === this.maxLevel) ? "T'es au max déjà !" : "You need " + (getXpForNextLevel(user.level) - user.exp) + " xp to level up !" }}</h2>
  </div>
</template>

<script>
export default {
  name: "expbar",
  props: {
    user: {
      type: Object,
      required: true
    },
    maxLevel: {
      type: Number,
      required: true
    }
  },
  methods: {
    getXpForNextLevel(level) {
      // Pokemon
      // return Math.round(4 * Math.pow(level, 3) / 5);

      // Classic
      return Math.round(5000 / 11 * (Math.pow(1.11, level - 1) - 1));
    },
    getXpPercent(exp, level) {
      if (level === this.maxLevel) {
        return 100;
      } else {
        //return exp * 100 / this.getXpForNextLevel(level);
        return exp * 100 / this.getXpForNextLevel(level);
      }
    }
  },
  updated: function() {
    this.$nextTick(function() {
      if (
        this.user.level < this.maxLevel &&
        this.user.exp >= this.getXpForNextLevel(this.user.level)
      ) {
        this.user.exp = this.user.exp - this.getXpForNextLevel(this.user.level);
        this.user.level += 1;
        alert("GG ! You are now lvl " + this.user.level);
      } else if (this.user.level === this.maxLevel) {
        this.user.exp = this.getXpForNextLevel(this.user.level);
      }
    });
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
.expbar {
  margin: 2rem auto;
  width: 90%;
  background-color: grey;
}
#expbar {
  height: 2rem;
  background-color: #4caf50;
  //  margin: 0 auto;
  vertical-align: center;
  line-height: 2rem; /* To center it vertically */
  color: white;
}
</style>
