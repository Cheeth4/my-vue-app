<template>
	<VCard footerClass="register-form__footer">
		<slot v-bind="form" v-if="isMounted"/>
		<template #footer>
			<slot name="footer" v-bind="{ submit: handleSubmit }"></slot>
		</template>
	</VCard>
</template>

<script setup lang="ts">
import VCard from "#/components/ui/VCard.vue";

import { useForm }    from 'vee-validate'
import { useMounted } from "@vueuse/core";

const emit = defineEmits<{
	(e: 'form-submit', values: Record<string, unknown>): void
}>();

const props = defineProps<{
	formData?: Record<string, any>
}>();

const form = useForm({
	initialValues: { ...props.formData }
});
const isMounted = useMounted();

const handleSubmit = () => {
	form.submitForm()
	form.validate().then(() => {
		if (form.meta.value.valid)
			emit('form-submit', form.values);
	})
}
</script>

<style lang="sass">
.register-form__footer
	display: flex
	gap: 8px
	padding-top: 40px
	flex-wrap: wrap

	> .button
		width: 100%

@include media(">mobile")
	.register-form__footer
		flex-wrap: nowrap
</style>