<template>
	<div class="box" :class="{ markable: markable && !marked }" v-on="!marked && markable ? { click : () => mark() } : {}">
		<div v-if="marked">{{ playerMark }}</div>
	</div>
</template>

<script>
export default {
	name: "TTTBox",
	props: {
		markable: {
			type: Boolean,
			default: false,
		},
	},
	
	data() {
		return {
			marked: false,
			p1Mark: false,
		}
	},

	computed: {
		playerMark() {
			return this.p1Mark ? 'X' : 'O'
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
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.markable:hover {
		background-color: lightgray;
		cursor: pointer;
	}
</style>