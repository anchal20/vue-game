<template lang="html">
					<div class="flipper">
						<div class="front">
						</div>
						<div class="back" v-bind:style="'background-color:' + color">
						</div>
					</div>
				</div>
</template>

<script>
var temp = [0];
export default {
	props: ['color'],
	data: function() {
		return {
			succesColors: [],
			selectedColor: [],
			currentColor: null
		}
	},
	computed: {
		colorCount: function() {
			return this.colorArray.length;
		}
	},
	beforeMount: function() {

	},
	mounted: function() {

	},
	created: function() {

	},
	methods: {
		selectBox: function(color) {
			// e.target.parentElement.parentElement.classList.toggle('hover');
			console.log(color['background-color']);
			var col = color['background-color'];
			this.selectedColor.push(col);
			console.log(this.selectedColor.length);
			if(this.selectedColor.length > 1) {
				if(this.selectedColor[0] == this.selectedColor[1]) {
					this.succesColors.push(this.selectedColor[0]);
					this.selectedColor = [];
				} else {
					this.selectedColor = [];
				}
			}
		},
		getRandomColor: function() {
			var random = 0;
			var colorArray = this.colorArray;
			var color = this.colorArray[random];
			colorArray.splice(random, 1);
			this.$set(this, color, color);
			this.$emit('setColorArray', colorArray);
			return {
				'background-color': color
			}

		}
	}
}
</script>

<style lang="css">

</style>
