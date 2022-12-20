<template>
	<div>
		<span>Welcome to Ultimate Tic Tac Toe!</span>
		<button @click="startGame = true">Play</button>
		<Play />
	</div>
</template>

<script>
import Play from './components/Play'

export default {
	name: 'App',
	components: {
		Play
	},
	data() {
		return {
			startGame: false,
		}
	}
}
</script>

<style>

</style>
