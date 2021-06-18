<template>
	<div class="my-form">
		<h2>{{ userForm.formTitle }}</h2>
		<form @submit.prevent="onSubmit">
			<div
				class="form-item"
				v-for="(item,idx) in userForm.formBase"
				:key="item.name"
			>
            <Input 
			:userInput="item"
            :idx="idx"
			@inputValidated="updateValidationStatus"/>
				
			</div>
			<Button
				type="submit"
				:color="userForm.submitButton.color"
				:isLoading="userForm.submitButton.isLoading"
				:text="userForm.submitButton.text"
			/>
		</form>
	</div>
</template>
<script>
import Button from './Button.vue'
import Input from './Input.vue'
export default {
	props: { userForm: Object },
	data() {
		return {
			formInputs: [],

		}
	},

	methods: {
		checkValidation(ev, validation, idx) {
			const res = validation(ev.target.value)
			this.formInputs[idx].validationStatus = res
			if (!res) this.formInputs[idx].showInvalidMsg = true
			else this.formInputs[idx].showInvalidMsg = false
		},
		onSubmit() {
			const form = {}
			this.formInputs.forEach((item, idx) => {
				const entry = this.userForm.formBase[idx].name
				if (item.validationStatus) { form[`${entry}`] = item.value }
			})
			if (Object.keys(form).length !== this.formInputs.length) return
			this.$emit('formSubmitted', this.formInputs)
		},
		styles(item) {
			if (item.validationStatus === null) return
			else return (item.validationStatus) ? 'valid' : 'invalid'
		},
		placeholderStyle(idx) {
			if (!this.formInputs[idx].value) return
			if (this.formInputs[idx].value.length) return {
				top: 0,
				fontSize: '12px',
				fontWeight: 'bold'
			}
		},
		updateValidationStatus(item,idx){
			this.formInputs[idx] = item
		}

	},
	created() {
		this.formInputs = this.userForm.formBase.map(item => {
			return { validation: item.validation, validationStatus: null, showInvalidMsg: true }
		})
	},
	components: { Button,Input }
}
</script>

<style>
@import url("https://cdn.d.greeninvoice.co.il/assets/web-app/2.2.331/components/webfonts/all.min.css");
.my-form {
	direction: rtl;
}
h2 {
	font-family: "almoni-neue-dl", sans-serif;
	font-size: 52px;
	color: #23445a;
	margin-bottom: 70px;
	letter-spacing: -2px;
}
form {
	font-family: "almoni-neue-dl", sans-serif;
	color: #23445a;
}
form > .form-item {
	position: relative;
	width: fit-content;
	padding: 1%;
	margin: 4% 0;
}
form button{
	direction: ltr;
}

</style>