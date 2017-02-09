<template>
  <div id="app">
    <hello></hello>
		<puzzle :rows="rows" :columns="columns"></puzzle>
  </div>
</template>

<script>
import Hello from './components/Hello'
import Puzzle from './components/Puzzle'

export default {
  name: 'app',
  components: {
    Hello,
		Puzzle
  },
	data: function() {
		return {
			rows: 4,
			columns: 3
		}
	}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
