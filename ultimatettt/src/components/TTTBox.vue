<template>
	<div class="box" :class="{unmarked: !marked }" @click="mark()">
		<div v-if="p1Mark">X</div>
		<div v-else-if="p2Mark">O</div>
	</div>
</template>

<script>
export default {
	name: "TTTBox",
	props: {
		top: {
			type: Boolean,
			default: false,
		},
		right: {
			type: Boolean,
			default: false,
		},
		bottom: {
			type: Boolean,
			default: false,
		},
		left: {
			type: Boolean,
			default: false,
		},
	},
	
	data() {
		return {
			marked: false,
			p1Mark: false,
			p2Mark: false,
		}
	},

	methods: {
		mark() {
			this.marked = true;
			if (this.$root.player1) {
				this.p1Mark = true;
				this.$emit("mark", 1);
			}
			else {
				this.p2Mark = true;
				this.$emit("mark", 2)
			}
			this.$root.player1 = !this.$root.player1;
		}
	}

}
</script>

<style scoped>
	.box {
		height: 5em;
		width: 5em;
	}
	.unmarked:hover {
		background-color: lightgray;
		cursor: pointer;
	}
	.top {
		border-top: 1px solid black;
	}
	.right {
		border-right: 1px solid black;
	}
	.bottom {
		border-right: 1px solid black;
	}
	.left {
		border-left: 1px solid black;
	}
</style>