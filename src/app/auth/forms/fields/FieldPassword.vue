<template>
	<FieldText v-model="model" :name="name" :label="label" :type="showPassword ? 'text' : 'password'">
		<template #append>
			<svg @pointerdown="handleEyePress" width="33" height="32" viewBox="0 0 33 32" fill="none"
				xmlns="http://www.w3.org/2000/svg">
				<path
					d="M16.5001 9.25102C12.4691 9.18302 8.30007 12 5.67907 14.885C5.40396 15.1905 5.25171 15.587 5.25171 15.998C5.25171 16.4091 5.40396 16.8056 5.67907 17.111C8.24307 19.935 12.4001 22.817 16.5001 22.748C20.6001 22.817 24.7581 19.935 27.3241 17.111C27.5992 16.8056 27.7514 16.4091 27.7514 15.998C27.7514 15.587 27.5992 15.1905 27.3241 14.885C24.7001 12 20.5311 9.18302 16.5001 9.25102Z"
					stroke="#5D5D67" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
				<path
					d="M20.25 16C20.2498 16.7417 20.0297 17.4666 19.6175 18.0831C19.2054 18.6997 18.6196 19.1802 17.9344 19.4639C17.2491 19.7475 16.4952 19.8217 15.7678 19.6768C15.0404 19.532 14.3723 19.1748 13.848 18.6503C13.3237 18.1258 12.9666 17.4576 12.822 16.7302C12.6774 16.0028 12.7517 15.2489 13.0355 14.5637C13.3194 13.8786 13.8001 13.293 14.4167 12.8809C15.0334 12.4689 15.7584 12.249 16.5 12.249C16.9926 12.2489 17.4804 12.3458 17.9355 12.5343C18.3905 12.7228 18.804 12.9991 19.1523 13.3474C19.5006 13.6958 19.7768 14.1094 19.9651 14.5645C20.1535 15.0196 20.2503 15.5074 20.25 16Z"
					stroke="#5D5D67" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
			</svg>
		</template>
	</FieldText>
</template>

<script lang="ts" setup>
import FieldText from "./FieldText.vue";

import { ref }            from "vue";
import { useEventListener, useVModel } from "@vueuse/core";

const props = defineProps<{
	modelValue?: string,
	required?: boolean,
	name: string,
	label: string,
}>()
const model = useVModel(props);

const showPassword = ref(false);

const handleEyePress = () => {
	showPassword.value = true;
}

useEventListener('pointerup', () => {
	showPassword.value = false
})
</script>

<style scoped>

</style>