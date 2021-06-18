<template>
	<div class="my-input">
		<input
			:class="styles(input)"
			:type="userInput.type"
			v-model="input.value"
			@change="checkValidation($event, userInput.validation)"
		/>
		<span :style="placeholderStyle(input)" class="input-placeholder"
			>{{ userInput.name }}
		</span>
		<p
			:style="{
				transform: input.showInvalidMsg ? 'scaleY(1)' : 'scaleY(0)',
				marginTop: '0',
				transition: 'all .3s ease',
				'margin-top':'5px'
			}"
		>
			{{ userInput.invalidMsg }}
		</p>
	</div>
</template>
<script>
export default {
	props: { userInput: Object , idx:Number},
	data() { return { input:{}} },
	methods: {
		checkValidation(ev, validation) {
			const res = validation(ev.target.value)
			this.input.validationStatus = res
			if (this.input.validationStatus) this.$emit('inputValidated', this.input,this.idx)
			if (!res) this.input.showInvalidMsg = true
			else this.input.showInvalidMsg = false
		},
		placeholderStyle(input) {
			if (!input.value) return
			else if (input.value.length) 
				return {
				top: '-15px',
				fontSize: '12px',
				fontWeight: 'bold'
			}
		},
		styles(input) {
			if (input.validationStatus === null) return
			else return (input.validationStatus) ? 'valid' : 'invalid'
		}
	},
	created() {
		this.input = { validation: this.userInput.validation, validationStatus: null, showInvalidMsg: true }
	}
}
</script>
<style>
.my-input {
	position: relative;
	width: fit-content;
}
.my-input input {
	transition: all 0.2s ease;
	outline: none;
	border: none;
	border-bottom: 1px solid #23445a;
	color: #23445a;
	font-size: 22px;
	line-height: 22px;
	z-index: 5;
	position: relative;
	background-color: transparent;
}
.my-input .input-placeholder {
	font-size: 22px;
	position: absolute;
	color: #23445a;
	top: -5px;
	right: 15px;
	transition: top 0.3s ease, right 0.3s ease, font-size 0.3s ease;
}
.my-input input:focus + .input-placeholder {
	top: -20px;
	font-size: 14px;
	font-weight: bold;
}
.my-input .invalid {
	border-color: #db2828;
}
.my-input .valid:focus {
	border-bottom: 2px solid #10bb69;
}
</style>