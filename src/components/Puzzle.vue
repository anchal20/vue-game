<template lang="html">
	<div class="">
		<div class="frame">
			<div class="rows" v-for="(row, rIndex) in rows">
				<div class="columns" v-for="(column, index) in columns" @click='selectBox($event)' :data-column="counter++" :data-row="rIndex">
					<div class="flipper">
						<div class="front">

						</div>
						<div class="back">

						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: ['rows', 'columns'],
	data: function() {
		return {
			counter: 0,
			color: {
				red: 0,
				blue: 0,
				green: 0
			}
		}
	},
	beforeMount: function() {

	},
	mounted: function() {

	},
	methods: {
		selectBox: function(e) {
			console.log(e.target.parentElement.parentElement);
			e.target.parentElement.parentElement.classList.toggle('hover');
		}
	}
}
</script>

<style lang="css">
	.frame {
		margin: 0 auto;
		border: 1px solid #000;
		max-width: 920px;
	}
	.rows {
		height: 100px;
		border-bottom: 1px solid #000;
		display: flex;
		flex-direction: row;
	}
	.columns {
		border: 1px solid #000;
		perspective: 1000px;
		flex-grow: 1;
		cursor: pointer;
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
		background-color: red;
	}
	.columns.hover .flipper {
		transform: rotateY(180deg);
	}
</style>
