<template>
  <div class="mainApp">
    <h1 id="gamesTitle">List Popular Videos Game</h1>
    <div class="gamesMain">
      <ul v-for="(game, i) in gameList[0]" :key="i">
        <div class="gamesInner">
          <li><img :src="game.background_image" alt="Game Images" /></li>
          <li class="gameName">{{ game.name }}</li>
          <li>Released: {{ game.released }}</li>
          <li>Rating: {{ game.rating }}</li>
        </div>
      </ul>
    </div>

    <button v-if="previousUrl !== null" @click="paginateBackGame">
      Previous Games
    </button>

    <button v-if="nextUrl !== null" @click="paginateForwardGame">
      Next Games
    </button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      gameList: [],
      nextUrl: null,
      previousUrl: null
    };
  },
  mounted() {
    this.fetchGames(
      "https://api.rawg.io/api/games?key=6a02d5f471754850afd028600eea0479&dates=2020-12-01,2020-12-31&platforms=18,1,7&page_size=10"
    );
  },
  methods: {
    fetchGames(url) {
      axios
        .get(url)
        .then(({ data }) => {
          this.nextUrl = data.next;
          this.previousUrl = data.previous;
          this.gameList = [];
          this.gameList.push(data.results);
        })

        .catch((error) => {
          console.log(error);
        });
    },
    paginateBackGame() {
      this.fetchGames(this.previousUrl);
    },
    paginateForwardGame() {
      this.fetchGames(this.nextUrl);
    }
  }
};
</script>

<style scoped>
.gamesMain {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.gameContainer {
  width: 100%;
  height: 300px;
  overflow: hidden;
}
#gamesTitle {
  color: #fff !important;
  font-weight: 700 !important;
  margin-bottom: 70px !important;
}
.gamesInner {
  background: #202020;
  border-radius: 20px;
  padding-bottom: 20px;
}
.gameName {
  font-weight: 900;
}
ul {
  width: 29%;
  list-style-type: none;
  margin-bottom: 50px !important;
}
ul li {
  color: #fff;
  margin-bottom: 10px;
}
ul li img {
  width: 100%;
  height: 150px;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}
</style>
