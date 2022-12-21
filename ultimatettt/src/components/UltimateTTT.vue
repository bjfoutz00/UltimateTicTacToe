<template>
	<div>
		<div>
			<div class="ttt-row">
				<TicTacToe
					class="one"
					:class="{ highlighted: isCurrent(0, 0), selectBox: selectBox }"
					:clickable="isCurrent(0, 0)"
					v-on="selectBox ? { click : () => move(0, 0) } : {}"
					@done="(player) => boxDone(0, 0, player)"
					@move="(i, j) => move(i, j)"
				/>
				<TicTacToe
					class="two"
					:class="{ highlighted: isCurrent(0, 1), selectBox: selectBox }"
					:clickable="isCurrent(0, 1)"
					v-on="selectBox ? { click : () => notify() } : {}"
					@done="(player) => boxDone(0, 1, player)"
					@move="(i, j) => move(i, j)"
				/>
				<TicTacToe
					class="three"
					:class="{ highlighted: isCurrent(0, 2), selectBox: selectBox }"
					:clickable="isCurrent(0, 2)"
					v-on="selectBox ? { click : () => move(0, 2) } : {}"
					@done="(player) => boxDone(0, 2, player)"
					@move="(i, j) => move(i, j)"
				/>
			</div>
			<div class="ttt-row">
				<TicTacToe
					class="four"
					:class="{ highlighted: isCurrent(1, 0), selectBox: selectBox }"
					:clickable="isCurrent(1, 0)"
					v-on="selectBox ? { click : () => move(1, 0) } : {}"
					@done="(player) => boxDone(1, 0, player)"
					@move="(i, j) => move(i, j)"
				/>
				<TicTacToe
					class="five"
					:class="{ highlighted: isCurrent(1, 1), selectBox: selectBox }"
					:clickable="isCurrent(1, 1)"
					v-on="selectBox ? { click : () => move(1, 1) } : {}"
					@done="(player) => boxDone(1, 1, player)"
					@move="(i, j) => move(i, j)"
				/>
				<TicTacToe
					class="six"
					:class="{ highlighted: isCurrent(1, 2), selectBox: selectBox }"
					:clickable="isCurrent(1, 2)"
					v-on="selectBox ? { click : () => move(1, 2) } : {}"
					@done="(player) => boxDone(1, 2, player)"
					@move="(i, j) => move(i, j)"
				/>
			</div>
			<div class="ttt-row">
				<TicTacToe
					class="seven"
					:class="{ highlighted: isCurrent(2, 0), selectBox: selectBox }"
					:clickable="isCurrent(2, 0)"
					v-on="selectBox ? { click : () => move(2, 0) } : {}"
					@done="(player) => boxDone(2, 0, player)"
					@move="(i, j) => move(i, j)"
				/>
				<TicTacToe
					class="eight"
					:class="{ highlighted: isCurrent(2, 1), selectBox: selectBox }"
					:clickable="isCurrent(2, 1)"
					v-on="selectBox ? { click : () => move(2, 1) } : {}"
					@done="(player) => boxDone(2, 1, player)"
					@move="(i, j) => move(i, j)"
				/>
				<TicTacToe
					class="nine"
					:class="{ highlighted: isCurrent(2, 2), selectBox: selectBox }"
					:clickable="isCurrent(2, 2)"
					v-on="selectBox ? { click : () => move(2, 2) } : {}"
					@done="(player) => boxDone(2, 2, player)"
					@move="(i, j) => move(i, j)"
				/>
			</div>
	</div>
	</div>
</template>

<script>
import TicTacToe from "./TicTacToe.vue"
export default {
	name: "UltimateTTT",
	components: {
		TicTacToe,
	},

	created() {
		for (let i = 0; i < 3; i++) {
			this.boxes.push([])
			for (let j = 0; j < 3; j++) {
				this.boxes[i].push(0);
			}
		}
		this.currRow = 0;
		this.currCol = 0;
	},

	data() {
		return {
			boxes: [],
			currRow: null,
			currCol: null,
			selectBox: false,
		}
	},

	methods: {
		playerMark(i, j) {
			return this.boxes[i][j] == 1 ? "X" : "O";
		},

		move(i, j) {
			console.log('move here!')
			this.selectBox = false;
			this.currRow = i;
			this.currCol = j;
			if (this.isDone(i, j)) {
				this.selectBox = true;
			}
		},

		notify() {
			console.log('notified!')
		},

		isCurrent(i, j) {
			return this.currRow == i && this.currCol == j;
		},

		isDone(i, j) {
			return this.boxes[i][j] != 0;
		},

		boxDone(i, j, player) {
			this.boxes[i][j] = player;
			this.checkEnd(i, j, player);
		},

		checkEnd(i, j, player) {
			if (this.checkRow(i, player)) return true;
			if (this.checkCol(j, player)) return true;
			if (this.checkDiag(player)) return true;
			return false;
		},

		checkRow(i, player) {
			for (let mark of this.boxes[i]) {
				if (mark != player) return false;
			}
			return true;
		},

		checkCol(j, player) {
			for (let row of this.boxes) {
				if (row[j] != player) return false;
			}
			return true;
		},

		checkDiag(player) {
			if (this.boxes[1][1] == player &&
				((this.boxes[0][0] == player && this.boxes[2][2] == player) ||
				(this.boxes[0][2] == player && this.boxes[2][0] == player))) {
					return true;
			}
			return false;
		}
	},

}
</script>

<style scoped>
	.highlighted {
		background-color: lightblue;
	}

	.selectBox:hover {
		background-color: lightgray;
	}

	.done-box {
		width: 244px;
		height: 244px;
	}

</style>