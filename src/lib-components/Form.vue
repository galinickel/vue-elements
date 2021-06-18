<template>
	<div class="my-form">
		<h2>{{ userForm.formTitle }}</h2>
		<form @submit.prevent="onSubmit">
			<div
				class="form-item"
				v-for="(item, idx) in userForm.formBase"
				:key="item.name"
			>
				<Input
					:userInput="item"
					:idx="idx"
					@inputValidated="updateValidationStatus"
				/>
			</div>
			<Button
				type="submit"
				:color="userForm.submitButton.color"
				:isLoading="userForm.submitButton.isLoading"
				:text="userForm.submitButton.text"
			/>
			<button class="google-btn">
				<img
					src="https://gist.githubusercontent.com/galinickel/c2bf93e06967b50ad1299baa0f139cbe/raw/e130de625d9c272f2a00efb0517c8a1523e17c5b/google-icon.svg"
				/>
				כניסה מהירה
			</button>
			<p v-show="showErr">{{ userForm.submitErrorMsg }}</p>
			<p class="form-footer">
				עוד לא הצטרפת? <span>ל-30 יום ניסיון חינם</span>
			</p>
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
			showErr: false
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
			if (Object.keys(form).length !== this.formInputs.length) {
				this.showErr = true
				return
			}
			this.$emit('formSubmitted', this.formInputs)
			this.showErr = false
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
		updateValidationStatus(item, idx) {
			this.formInputs[idx] = item
		}

	},
	created() {
		this.formInputs = this.userForm.formBase.map(item => {
			return { validation: item.validation, validationStatus: null, showInvalidMsg: true }
		})
	},
	components: { Button, Input }
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
	letter-spacing: -3px;
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
.form-item:nth-child(2) > div p {
	text-decoration: underline;
	cursor: pointer;
}
form input {
	width: 420px;
}
form button {
	direction: ltr;
}

.google-btn {
	height: 56px;
	width: 172px;
	display: inline-flex;
	align-items: center;
	justify-content: space-evenly;
	border-radius: 100px;
	border: 1px solid #0084f4;
	cursor: pointer;
	font-family: "almoni-neue-dl", sans-serif;
	color: #0084f4;
	font-size: 18px;
	font-weight: bold;
	letter-spacing: 0;
	line-height: 20px;
	text-align: center;
	background-color: transparent;
	margin-right: 30px;
}
.google-btn img {
	height: 24px;
	width: 24px;
}
.form-footer {
	color: #0084f4;
	font-size: 22px;
	letter-spacing: -0.5px;
	font-weight: 400;
}
.form-footer span {
	border-bottom: 1px solid #0084f4;
}
</style>