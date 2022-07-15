<template>
	<RegisterStep>
		<template v-slot="{ values }">
			<FieldText v-model="values.email" :rules="[
					{ validateFn: email,            text: 'This email is invalid' },
					{ validateFn: isMonterailEmail, text: 'The email must ends with monterail.com' }
				]"
				label="email"
				name="email"
				placeholder="Something ending with monterail.com"
				required
			/>
			<FieldPassword v-model="values.password" :hints="[
					{ validateFn: atLeast8Chars,    text: 'At least 8 characters' },
			    { validateFn: atLeastOneLetter, text: 'At least one letter' },
			    { validateFn: atLeastOneDigit,  text: 'At least one digit' }
				]"
				label="Password"
				name="password"
				placeholder="Enter your password"
				required
			/>
		</template>
		<template #footer="{ submit }">
			<VButton flat>Log in instead</VButton>
			<VButton @click="submit">Next step</VButton>
		</template>
	</RegisterStep>
</template>

<script lang="ts" setup>
import RegisterStep from "../RegisterStep.vue";

import FieldText     from "./fields/FieldText.vue";
import FieldPassword from "./fields/FieldPassword.vue";

import VButton from "#/components/form/VButton.vue";

import { email } from "@vee-validate/rules";

const isMonterailEmail = (v: string) => v.toLocaleLowerCase().endsWith('monterail.com')

const atLeast8Chars    = (v: string) => v.length >= 8
const atLeastOneLetter = (v: string) => v.match('.*[a-zA-Z]')
const atLeastOneDigit  = (v: string) => v.match('.*[0-9]')
</script>
