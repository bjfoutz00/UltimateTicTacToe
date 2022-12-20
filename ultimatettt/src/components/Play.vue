<template>
	<div>
		<div class="ttt-container">
			<div class="ttt-row">
				<TTTBox class="one" @mark="(player) => setMark(0, 0, player)"/>
				<TTTBox class="two" @mark="(player) => setMark(0, 1, player)"/>
				<TTTBox class="three" @mark="(player) => setMark(0, 2, player)"/>
			</div>
			<div class="ttt-row">
				<TTTBox class="four" @mark="(player) => setMark(1, 0, player)"/>
				<TTTBox class="five" @mark="(player) => setMark(1, 1, player)"/>
				<TTTBox class="six" @mark="(player) => setMark(1, 2, player)"/>
			</div>
			<div class="ttt-row">
				<TTTBox class="seven" @mark="(player) => setMark(2, 0, player)"/>
				<TTTBox class="eight" @mark="(player) => setMark(2, 1, player)"/>
				<TTTBox class="nine" @mark="(player) => setMark(2, 2, player)"/>
			</div>
		</div>
		<div v-if="end">{{ currPlayer }} wins!</div>
	</div>
</template>

<script>
import TTTBox from "./TTTBox.vue"
export default {
	name: "Play",
	components: {
		TTTBox,	
	},

	created() {
		for (let i = 0; i < 3; i++) {
			this.boxes.push([])
			for (let j = 0; j < 3; j++) {
				this.boxes[i].push(0);
			}
		}
		console.log(this.boxes)
	},

	data() {
		return {
			boxes: [],
			end: false,
			currPlayer: "Player 1"
		}
	},

	computed: {
	},

	methods: {
		setMark(i, j, player) {
			if (player == 1) this.currPlayer = "Player 1";
			else this.currPlayer = "Player 2";
		
			this.boxes[i][j] = player;
			this.end = this.checkEnd(i, j, player);
			console.log(this.end)
		},

		checkEnd(i, j, player) {
			if (this.checkRow(i, player)) return true;
			if (this.checkCol(j, player)) return true;
			if (this.checkDiag(i, j, player)) return true;
			return false;
		},

		checkRow(i, player) {
			for (let mark in this.boxes[i]) {
				if (mark != player) return false;
			}
			return true;
		},

		checkCol(j, player) {
			for (let row in this.boxes) {
				if (this.boxes[row][j] != player) return false;
			}
			return true;
		},

		checkDiag(val) {
			if (this.boxes[1, 1] == val && 
				this.boxes[0, 0] == val && this.boxes[2, 2] == val ||
				this.boxes[2, 2] == val && this.boxes[0, 0] == val) {
				
				return true;
			}
			return false;
		}
	}
}
</script>

<style scoped>
/* .ttt-container {
	display: flex;
	flex-wrap: wrap;
	align-items: center;
	justify-content: center;
} */
.ttt-row {
	display: flex;
}
.one {
	border-right: 1px solid black;
	border-bottom: 1px solid black;
}
.two {
	border-right: 1px solid black;
	border-bottom: 1px solid black;
	border-left: 1px solid black; 
}
.three {
	border-bottom: 1px solid black;
	border-left: 1px solid black; 
}
.four {
	border-top: 1px solid black;
	border-right: 1px solid black;
	border-bottom: 1px solid black;
}
.five {
	border-top: 1px solid black;
	border-right: 1px solid black;
	border-bottom: 1px solid black;
	border-left: 1px solid black; 
}
.six {
	border-top: 1px solid black;
	border-bottom: 1px solid black;
	border-left: 1px solid black; 
}
.seven {
	border-top: 1px solid black;
	border-right: 1px solid black;
}
.eight {
	border-top: 1px solid black;
	border-right: 1px solid black;
	border-left: 1px solid black; 
}
.nine {
	border-top: 1px solid black;
	border-left: 1px solid black; 
}


</style>