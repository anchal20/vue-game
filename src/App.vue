<template>
  <div id="app">
    <hello></hello>
		<p>Enter the row and column (product of row and column should be a multilple of 2) </p>
		<input v-model.number="rows">
		<input v-model.number="columns">
		<br>
		<br>
		<div class="wrapper">
			<div class="rows" >
				<div class="columns" v-for="(block, index) in blocks"
				@click.prevent="activeColors.includes(backgroundColors[index]) || selectedIndx.includes(index) ? 'null' : flipCard(index)"
				:class="{
					active: activeColors.includes(backgroundColors[index]),
					selected: selectedIndx.includes(index)
					}">
					<puzzle :color="backgroundColors[index]" ></puzzle>
				</div>
			</div>
		</div>
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
			columns: 3,
			backgroundColors: [],
			activeColors: [],
			selectedIndx: [],
      cardFlipped: 0
		}
	},
	computed: {
		blocks: function() {
			return (this.rows * this.columns);
		}
	},
	created: function() {
		this.setBackgroundColors();
	},
	watch: {
		rows: function() {
			this.reset();
			this.resetRowColumn();
		},
		columns: function() {
			this.reset();
			this.resetRowColumn();
		},
    cardFlipped: function() {
      let blocks = (this.rows * this.columns)/2;
      if(this.cardFlipped == blocks) {
        setTimeout(() => {
          alert("Congrats! You have won the game!");
          this.reset();
          this.cardFlipped = 0;
        }, 1000);

      }
    }
	},
	methods: {
		setBackgroundColors: function() {
			var colorArray = this.getColorArray();
			this.$set(this, 'backgroundColors', colorArray);
		},
		getColorArray: function() {
			let blocks = (this.rows * this.columns)/2;
			let colorArray = [];
			for(var i=0; i < blocks; i++) {
				let red = Math.round(Math.random() * 256);
				let blue = Math.round(Math.random() * 256);
				let green = Math.round(Math.random() * 256);
				let color = "rgb(" + red + "," + blue + "," + green + ")";
				colorArray.push(...[color, color]);
				// colorArray.push(color);
			}
			//this.$set(this, colorArray, colorArray);
			var counter = colorArray.length, temp, index;
	   	// While there are elements in the array
	   	while (counter > 0) {
        	// Pick a random index
        	index = Math.floor(Math.random() * counter);
        	// Decrease counter by 1
        	counter--;
        	// And swap the last element with it
        	temp = colorArray[counter];
        	colorArray[counter] = colorArray[index];
        	colorArray[index] = temp;
	    	}
			return colorArray;
		},

		setColorArray: function(array) {
			this.$set(this, colorArray, array);
		},
		flipCard: function(index) {
			if(!this.selectedIndx.length) {
				this.selectedIndx.push(index);
			} else {
				if(this.backgroundColors[index] == this.backgroundColors[this.selectedIndx[0]]) {
					this.activeColors.push(this.backgroundColors[index]);
					this.selectedIndx = [];
          this.cardFlipped++;
				} else {
					this.selectedIndx.push(index);
					setTimeout(() => {
						this.selectedIndx = [];
					}, 1000);
				}
			}
		},
		reset: function() {
			this.setBackgroundColors();
			this.activeColors = [],
			this.selectedIndx = []
		},
		resetRowColumn: function() {
			if(this.blocks%2 !== 0) {
				alert('Only even number of blocks are allowed, Your puzzle is reset to original value');
				this.reset();
				this.rows = 4;
				this.columns = 3;
			}
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
.wrapper {
	max-width: 600px;
	margin: 0 auto;
}
.rows {
	display: flex;
	flex-wrap: wrap;
	flex: 1;
	justify-content: center;
}
.columns {
	border: 1px solid #000;
	perspective: 1000px;
	display: flex;
	cursor: pointer;
	width: 25%;
	height: 50px;
}
.flipper {
	transition: 0.6s;
	transform-style: preserve-3d;
	position: relative;
}
.flipper, .front, .back {
	width: 100%;
	height: 100%;
}
.front, .back {
	backface-visibility: hidden;
	position: absolute;
	top: 0;
	left: 0;
}
.front {
	z-index: 2;
	transform: rotateY(0deg);
	background-color: pink;
}
.back {
	transform: rotateY(180deg);
}
.columns.active .flipper, .columns.selected .flipper {
	transform: rotateY(180deg);
}
</style>
