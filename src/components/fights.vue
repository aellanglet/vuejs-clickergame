<template>
  <div>
    <button v-on:click="getAMonster(user.level, localMonsters)">un monstre !</button>
    <div v-if="monster">
      <h2>{{monster.name}}</h2>
      <img width="25%" :src="monster.img" v-on:click="attack(user, monster)">
      <ul>
        <li >Pv : {{ monster.health }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "fights",
  data() {
    return {
      localMonsters: JSON.parse(JSON.stringify(this.monsters)),
      monster: ""
    };
  },
  props: {
    user: {
      type: Object,
      required: true
    },
    monsters: {
      type: Array,
      required: true
    },
    maxLevel: {
      type: Number,
      required: true
    }
  },
  methods: {
    getAMonster(userLvl, monsters) {
      //monsters = JSON.parse(monsters);
      let filteredMonsters = monsters.filter(monster => {
        return monster.lvlMin <= userLvl && monster.lvlMax >= userLvl;
      });

      this.monster =
        filteredMonsters[Math.floor(Math.random() * filteredMonsters.length)];

      //this.monster.health = this.monster.health();
      //this.monster.exp = this.monster.exp();
      //console.log(this.monster);
      if (event) {
        this.randomizeHealthXp();
      }
    },
    attack(user, monster) {
      monster.health = monster.health - user.stats.strengh;
      console.log(monster.health);
      if (monster.health <= 0) {
        user.exp += monster.exp;
        user.totalExp += monster.exp;
        this.getAMonster(user.level, this.localMonsters);
      }
    },
    randomizeHealthXp() {
      this.monsters.forEach((aMonster, index) => {
        //console.log(this.localMonsters[index].health());
        //console.log(this.monsters[index].health);
        let health = aMonster.health();
        //this.monsters[index].health();
        let exp = aMonster.exp();
        // this.monsters[index].exp();

        this.localMonsters[index].health = health;
        this.localMonsters[index].exp = exp;
      });
    }
  },
  updated: function() {
    this.$nextTick(function() {
      if (this.monster) {
        //console.log(this.monster);
        if (this.monster.health <= 0) {
          //console.log(this.user.exp);
        }
      }
    });
  },
  created: function() {
    this.randomizeHealthXp();
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
