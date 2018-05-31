<template>
  <div id="app">
  <img width="25%" src="./assets/logo.png" v-on:click="addMoreOffAllResources">
    <accueil/>
    <score :resources="resources" :user="user" :maxLevel="maxLevel"/>
    <expbar :user="user" :maxLevel="maxLevel"/>
    <fights :user="user" :maxLevel="maxLevel" :monsters="monsters"/>
  </div>
</template>

<script>
import accueil from "./components/accueil";
import score from "./components/score";
import expbar from "./components/expbar";
import fights from "./components/fights";

export default {
  name: "App",
  components: {
    accueil,
    score,
    expbar,
    fights
  },
  data() {
    return {
      title: "app",
      resources: { wood: 0, gold: 0, food: 0 },
      user: {
        name: "Aël",
        level: 1,
        stats: {
          strengh: 2
        },
        exp: 0,
        totalExp: 0
      },
      maxLevel: 60,
      maxResources: 99999,
      monsters: [
        {
          name: "Troll",
          img:
            "https://i.pinimg.com/originals/0e/76/86/0e76866908034ee0abe23100ed280c2c.jpg",
          health: function() {
            return Math.floor(Math.random() * (55 - 40 + 1)) + 40;
          },
          exp: function() {
            return Math.floor(Math.random() * (10 - 5 + 1)) + 5;
          },
          lvlMin: 5,
          lvlMax: 15
        },
        {
          name: "Gobelin",
          img:
            "https://i.pinimg.com/originals/ae/11/51/ae11519563ce76d886145318c8772f29.jpg",
          health: function() {
            return Math.floor(Math.random() * (35 - 25 + 1)) + 25;
          },
          exp: function() {
            return Math.floor(Math.random() * (6 - 3 + 1)) + 3;
          },
          lvlMin: 1,
          lvlMax: 15
        },
        {
          name: "Orc",
          img:
            "https://i.pinimg.com/originals/11/60/60/1160600f9aacd80c34eec07f6c8d7622.jpg",
          health: function() {
            return Math.floor(Math.random() * (90 - 70 + 1)) + 70;
          },
          exp: function() {
            return Math.floor(Math.random() * (15 - 8 + 1)) + 8;
          },
          lvlMin: 10,
          lvlMax: 20
        },
        {
          name: "Rat",
          img:
            "https://i.pinimg.com/originals/7d/50/89/7d5089da6bf0f8ee94f04f89d7836b92.jpg",
          health: function() {
            return Math.floor(Math.random() * (12 - 8 + 1)) + 8;
          },
          exp: function() {
            return Math.floor(Math.random() * (3 - 1 + 1)) + 1;
          },
          lvlMin: 1,
          lvlMax: 10
        },
        {
          name: "Spider",
          img:
            "https://i.pinimg.com/originals/94/ab/da/94abda41ad5a7d9cb2a2bac22dc306e8.jpg",
          health: function() {
            return Math.floor(Math.random() * (23 - 15 + 1)) + 15;
          },
          exp: function() {
            return Math.floor(Math.random() * (4 - 2 + 1)) + 2;
          },
          lvlMin: 1,
          lvlMax: 20
        }
      ]
    };
  },
  created: function() {
    //    setInterval(() => {
    //      this.resources.food += 2;
    //      this.resources.wood += 2;
    //      this.resources.gold++;
    //    }, 1500);
    //console.log(expbar);
  },
  methods: {
    addMoreOffAllResources() {
      Object.keys(this.resources).forEach(resource => {
        this.resources[resource] += 100;
      });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
