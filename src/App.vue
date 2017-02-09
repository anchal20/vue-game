<template>
  <div id="app">
    <hello></hello>
		<p>Enter the row and column (product of row and column should be a multilple of 2) </p>
		<input v-model.number="rows">
		<input v-model.number="columns">
		<br>
		<br>
		<puzzle :rows="rows" :columns="columns" :colorArray="getColorArray"></puzzle>
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
	},
	computed: {
		getColorArray: function() {
			let blocks = (this.rows * this.columns)/2;
			let colorArray = [];
			for(var i=0; i < blocks; i++) {
				let red = Math.round(Math.random() * 256);
				let blue = Math.round(Math.random() * 256);
				let green = Math.round(Math.random() * 256);
				let color = "rgb(" + red + "," + blue + "," + green + ")";
				colorArray.push(color);
				colorArray.push(color);
			}
			console.log(colorArray);
			//this.$set(this, colorArray, colorArray);
			return colorArray;
		}
	},
	created: function() {

	},
	methods: {

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
