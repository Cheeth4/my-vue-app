<template>
	<label>
		<div :class="['checkbox', { error: isError }]">
			<input v-bind="$attrs" type="checkbox" v-model="model" />
			<div class="checkbox__box">
				<div class="checkbox__mark" v-if="modelValue"></div>
			</div>
		</div>
		<span class="checkbox__label" :style="{ color: isError ? 'red' : ''}">
			<slot>{{ label }}</slot>
		</span>
	</label>
</template>

<script  lang="ts">
export default {
	inheritAttrs: false
}
</script>
<script setup lang="ts">
import { defineProps } from "vue";
import { useVModel }   from "@vueuse/core";

const props = defineProps<{
	isError?: boolean,
	modelValue?: boolean | string[],
	label?: string,
	required?: boolean,
}>()
const model = useVModel(props)

</script>

<style lang="sass" scoped>
label
	display: inline-flex
	align-items: center

.checkbox

	> input[type="checkbox"]
		position: absolute
		opacity: 0
		width: 0
		height: 0
		border: 0
		padding: 0

	&.error > &__box
		border-color: red

.checkbox__box
	cursor: pointer
	position: relative
	width: 24px
	height: 24px
	border: 1px solid #AEAEB3
	border-radius: 8px

.checkbox__mark
	position: absolute
	width: 6px
	height: 12px
	transform: rotate(45deg)
	border-right: 2px solid #F47073
	border-bottom: 2px solid #F47073
	top: 4px
	left: 8px

.checkbox__label
	margin-left: 8px
	font-size: 18px
	font-family: Roboto, serif
	
</style>