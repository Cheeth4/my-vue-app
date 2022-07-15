<template>
	<div class="input__wrapper">
		<div class="input__label">
			{{ label }}
		</div>
		<div class="input__input">
			<input v-model="model" v-bind="$attrs"
				:class="{ error: isError }"/>
			<div class="input__append">
				<slot name="append"/>
			</div>
		</div>
		<div class="input__hint" v-if="$slots.hint">
			<slot name="hint"></slot>
		</div>
		<div class="input__errors">
			<slot name="errors"></slot>
		</div>
	</div>
</template>

<script lang="ts">
export default {
	inheritAttrs: false
}
</script>
<script setup lang="ts">
import { defineProps } from "vue";

import { useVModel } from "@vueuse/core";

const props = defineProps<{
	inputProps?: any,
	lazy?: boolean,
	label: string,
	modelValue?: string,
	isError?: boolean,
	required?: boolean,
}>()
const model = useVModel(props)
</script>

<style lang="sass" scoped>
.input__label
	color: #F47073
	text-transform: uppercase
	font-weight: 700
	font-family: 'Roboto Mono', serif
	font-size: 14px
	margin-bottom: 12px

.input__input
	position: relative
	display: flex
	align-items: center

input
	width: 100%
	border: 1px solid transparent
	font-family: Roboto, serif
	color: #343541
	background-color: #F7F7F7
	border-radius: 8px
	font-size: 18px
	padding: 16px 24px
	outline: none

	&::placeholder
		color: #85868D

	&:hover
		background-color: #E5E5E5

	&:active, &:focus
		background-color: rgba(47, 128, 237, 0.1)
		border-color: #2F80ED

	&.error:not(:focus)
		border-color: #EC1115

.input__append
	display: inline-flex
	position: absolute
	right: 0
	margin-right: 12px


.input__hint, .input__errors
	font-family: Roboto, serif

.input__hint
	color: #343541
	margin-top: 8px
	line-height: 24px
	font-size: 14px

.input__errors
	padding-top: 3px
	min-height: 18px
	color: #EC1115
	font-size: 12px

</style>