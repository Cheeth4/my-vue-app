<template>
	<RegisterStep>
		<template v-slot="{ values }">
			<FieldText required v-model="values.firstName"
				name="firstName"
				label="First name"
				placeholder="e.g. Jessica"
			/>
			<FieldText required v-model="values.lastName"
				name="lastName"
				label="Last name"
				placeholder="e.g. Walton"
			/>
			<FieldText required v-model="values.birthDate"
				name="birthDate"
				label="Date of birth"
				placeholder="DD / MM / YYYY"
				type="date"
				:hints="[
					{ validateFn: isMinimum18,  text: 'You must be minimum 18 years old'}
				]"
			/>
			<Field name="accept" v-slot="{ field, errorMessage, meta }" :rules="v => v">
				<VCheckbox v-bind="field" v-model="values.accept" :is-error="!!errorMessage">
					I accept <u>Privacy Policy</u>
				</VCheckbox>
			</Field>
		</template>
		<template #footer="{ submit }">
			<VButton flat>Log in instead</VButton>
			<VButton @click="submit">Register</VButton>
		</template>
	</RegisterStep>
</template>

<script setup lang="ts">
import RegisterStep from "../RegisterStep.vue";

import FieldText from "./fields/FieldText.vue";
import VButton   from "#/components/form/VButton.vue";
import VCheckbox from "#/components/form/VCheckbox.vue";

import { Field } from "vee-validate";

const isMinimum18 = (dateString: string) => {
	const
		currentDate = new Date(Date.now()),
		birthDate   = new Date(dateString);

	let years = currentDate.getFullYear() - birthDate.getFullYear();

	const
		sameMonth        = currentDate.getMonth() === birthDate.getMonth(),
		furtherMonth     = currentDate.getMonth() < birthDate.getMonth(),
		sameOrFurtherDay = currentDate.getDate() < birthDate.getDate();

	if (furtherMonth || (sameMonth && sameOrFurtherDay))
		years -= 1

	return years >= 18
}
</script>
