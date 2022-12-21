<template>
	<div>
		<span>Welcome to Ultimate Tic Tac Toe!</span>
		<button @click="startGame = true">Play</button>
		<UltimateTTT />
	</div>
</template>

<script>
import UltimateTTT from './components/UltimateTTT'

export default {
	name: 'App',
	components: {
		UltimateTTT
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
