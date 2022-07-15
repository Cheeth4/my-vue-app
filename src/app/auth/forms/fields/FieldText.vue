<template>
	<Field validateOnInput :name="name" v-slot="{ field, errorMessage, meta }" :rules="fieldRules">
		<VInput :is-error="!!errorMessage" v-bind="{ ...field, ...$attrs }" v-model="model" :label="label" >
			<template #hint v-if="hints">
				<div v-for="hint in hints"
					:style="{ color: hint.validateFn(model) ? 'green' : meta.touched ? 'red' : '#343541' }">
					{{ hint.text }}
				</div>
			</template>
			<template #errors v-if="!hints && meta.touched">
				{{ errorMessage }}
			</template>

			<template #append>
				<slot name="append" />
			</template>
		</VInput>
	</Field>
</template>

<script lang="ts" setup>
import VInput    from "#/components/form/VInput.vue";
import { Field } from "vee-validate";

import { useVModel }   from "@vueuse/core";

type FieldRule = {
	text: string,
	validateFn: (v?: string) => string | boolean,
};

const props = defineProps<{
	modelValue?: string,
	required?: boolean,
	name: string,
	label: string,
	rules?: FieldRule[]
	hints?: FieldRule[]
}>();

const model = useVModel(props);

const fieldRules = (value?: string) => {
	const { required, rules, hints } = props;

	if (required && !value)
		return 'This field is required';

	const brokenRule = rules?.find(rule => !rule.validateFn(value));

	if (brokenRule)
		return brokenRule.text;

	return !hints?.some(rule => !rule.validateFn(value));
}
</script>

<style scoped>

</style>