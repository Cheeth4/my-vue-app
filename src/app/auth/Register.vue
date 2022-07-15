<template>
	<div class="register" v-if="!isFinished">
		<div class="title">{{ currentStep.title }}</div>
		<div class="subtitle">{{ currentStep.subtitle }}</div>
		<div class="register__forms">
			<component @form-submit="handleStepComplete" :formData="formData" :is="currentStep.component"/>
		</div>
	</div>
	<div class="success-screen" v-else>
		<div class="title">Good job {{ formData.firstName }}!</div>
		<div class="success-screen__info">
			<div>We have sent you an email to <b>{{ formData.email }}</b>. </div>
			<div>Make sure to click the link from the message to activate your account.</div>
		</div>
		<VButton class="success-screen__button" @click="reset">Go to homepage</VButton>
	</div>

</template>

<script setup lang="ts">
import FormCredentials from "./forms/FormCredentials.vue";
import FormUser        from "./forms/FormUser.vue";

import { markRaw, reactive, ref } from "vue";
import { computedEager }          from "@vueuse/shared";
import VButton                    from "#/components/form/VButton.vue";

const steps = [
	{
		title: 'Ahoy you!',
		subtitle: 'Care to register?',
		component: markRaw(FormCredentials)
	},
	{
		title: 'Great!',
		subtitle: 'Now your name',
		component: markRaw(FormUser)
	}
]

const isFinished = ref(false);

const currentStepIndex = ref<number>(0);
const currentStep = computedEager(() => steps[currentStepIndex.value])

const initialFormData = {
	email: '',
	password: '',
	firstName: '',
	lastName: '',
	birthDate: ''
}
const formData = reactive({ ...initialFormData })

const handleStepComplete = (values: Record<string, unknown>) => {
	Object.assign(formData, values);

	if (currentStepIndex.value >= steps.length - 1) {
		isFinished.value = true;
		return;
	}
	currentStepIndex.value++;
}

const reset = () => {
	Object.assign(formData, initialFormData);

	currentStepIndex.value = 0;
	isFinished.value = false;
}
</script>

<style lang="sass">
.title, .subtitle
	font-family: "Eczar", serif
	font-weight: 600
	font-size: 40px
	text-align: center
	letter-spacing: -0.01em
	line-height: 102%

.title
	color: #343541

.subtitle
	color: gray

.register__forms
	margin-top: 40px
	position: relative

.success-screen, .success-screen .title
	text-align: center

.success-screen__info
	font-family: Roboto, serif
	margin-top: 40px
	margin-bottom: 40px
	line-height: 21px
	font-size: 18px

	> div
		display: inline


@include media(">mobile")
	.title, .subtitle
		font-size: 80px
		text-align: left

	.success-screen__info > div
		display: block
</style>