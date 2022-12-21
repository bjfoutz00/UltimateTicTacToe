<template>
	<div>
		<div class="ttt-container">
			<div v-if="done" style="font-size: 5em;">{{ winnerSymbol }}</div>
			<div v-else>
				<div class="ttt-row">
					<TTTBox :markable="clickable" @mark="(player) => setMark(0, 0, player)" class="one"/>
					<TTTBox :markable="clickable" @mark="(player) => setMark(0, 1, player)" class="two"/>
					<TTTBox :markable="clickable" @mark="(player) => setMark(0, 2, player)" class="three"/>
				</div>
				<div class="ttt-row">
					<TTTBox :markable="clickable" @mark="(player) => setMark(1, 0, player)" class="four"/>
					<TTTBox :markable="clickable" @mark="(player) => setMark(1, 1, player)" class="five"/>
					<TTTBox :markable="clickable" @mark="(player) => setMark(1, 2, player)" class="six"/>
				</div>
				<div class="ttt-row">
					<TTTBox :markable="clickable" @mark="(player) => setMark(2, 0, player)" class="seven"/>
					<TTTBox :markable="clickable" @mark="(player) => setMark(2, 1, player)" class="eight"/>
					<TTTBox :markable="clickable" @mark="(player) => setMark(2, 2, player)" class="nine"/>
				</div>
			</div>
		</div>
		<!-- <div v-if="done">{{ currPlayer }} wins!</div> -->
	</div>
</template>

<script>
import TTTBox from "./TTTBox.vue"
export default {
	name: "Play",
	components: {
		TTTBox,	
	},

	props: {
		clickable: {
			type: Boolean,
			default: false,
		}
	},

	created() {
		for (let i = 0; i < 3; i++) {
			this.boxes.push([])
			for (let j = 0; j < 3; j++) {
				this.boxes[i].push(0);
			}
		}
	},

	data() {
		return {
			boxes: [],
			done: false,
			currPlayer: "Player 1",
			winner: 0,
		}
	},

	computed: {
		winnerSymbol() {
			return this.winner == 1 ? "X" : "O";
		}
	},

	methods: {
		setMark(i, j, player) {
			if (player == 1) this.currPlayer = "Player 1";
			else this.currPlayer = "Player 2";
		
			this.boxes[i][j] = player;
			if (this.checkDone(i, j, player)) {
				this.done = true;
				this.winner = player;
				this.$emit("done", player);
			}
			this.$emit("move", i, j);
		},

		checkDone(i, j, player) {
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
	}
}
</script>

<style>
.ttt-container {
	margin: 1em;
	width: 250px;
	height: 250px;
	display: flex;
	justify-content: center;
	align-items: center;
}

</style>