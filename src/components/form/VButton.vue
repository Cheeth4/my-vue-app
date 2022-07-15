<template>
	<button :class="['button', { flat }]">
		<slot />
	</button>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

defineProps<{
	flat?: boolean
}>()
</script>

<style lang="sass" scoped>
.button
	cursor: pointer
	font-family: "Roboto Mono", serif
	padding: 19px 32px
	font-weight: 500
	font-size: 18px
	background-color: #EC1115
	border-radius: 64px
	color: white
	border: none

	&:hover
		background-color: #A60C0E

	&:active
		outline: 5px solid #F47073

	&.flat
		background-color: transparent
		color: #EC1115

</style>