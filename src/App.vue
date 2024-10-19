<!-- App.vue -->
<template>
  <div id="app">
    <h1>Game Leaderboard</h1>
    <table>
      <thead>
        <tr>
          <th>Rank</th>
          <th>Player</th>
          <th>Stars</th>
          <th v-if="isAdmin">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(player, index) in sortedPlayers" :key="player.id">
          <td>{{ index + 1 }}</td>
          <td>{{ player.name }}</td>
          <td>{{ player.stars }}</td>
          <td v-if="isAdmin">
            <button @click="addStar(player.id)">+</button>
            <button @click="removeStar(player.id)">-</button>
          </td>
        </tr>
      </tbody>
    </table>
    <button @click="toggleAdmin">{{ isAdmin ? 'Exit Admin Mode' : 'Enter Admin Mode' }}</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      players: [
        {id: 1, name: 'Chiến Lỏ', stars: 5},
        {id: 2, name: 'Phúc Xô', stars: 3},
        {id: 3, name: 'Khoa Ozil', stars: 7},
        {id: 4, name: 'Hải Đây Lè', stars: 2},
        {id: 5, name: 'Pe Tẻ', stars: 6}
      ],
      isAdmin: false
    }
  },
  computed: {
    sortedPlayers () {
      return [...this.players].sort((a, b) => b.stars - a.stars)
    }
  },
  methods: {
    addStar (playerId) {
      const player = this.players.find(p => p.id === playerId)
      if (player) player.stars++
    },
    removeStar (playerId) {
      const player = this.players.find(p => p.id === playerId)
      if (player && player.stars > 0) player.stars--
    },
    toggleAdmin () {
      this.isAdmin = !this.isAdmin
    }
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

button {
  margin: 0 5px;
  padding: 5px 10px;
  cursor: pointer;
}
</style>
