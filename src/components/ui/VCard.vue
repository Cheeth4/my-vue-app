<template>
	<div class="card">
		<slot />
		<div class="card__footer" v-if="$slots.footer" :class="footerClass">
			<slot name="footer" />
		</div>
	</div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

defineProps<{
	footerClass?: string
}>()
</script>

<style lang="sass" scoped>
.card
	padding: 8px 16px

@include media(">mobile")
	.card
		width: 600px
		padding: 64px
		border-radius: 24px
		box-shadow: 0 4px 22px 0 #34354126

</style>