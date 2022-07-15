<template>
	<AppHeader />
	<div class="app-view">
		<Register />
	</div>
</template>

<script setup lang="ts">
import AppHeader from "./components/static/AppHeader.vue";
import Register  from "./app/auth/Register.vue";
</script>

<style lang="sass">
*
	box-sizing: border-box

body, html, #app
	width: 100%
	height: 100%
	padding: 0
	margin: 0

#app
	display: flex
	flex-direction: column
	color: #2c3e50
	font-family: Eczar, serif

.app-view
	display: flex
	justify-content: center
	align-items: center
	width: 100%
	height: 100%
</style>
