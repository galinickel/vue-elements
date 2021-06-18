<template>
	<button :style="{ backgroundColor: color }" class="my-button" >
		<p>
			<img
				:style="{ visibility: isLoading ? 'visible' : 'hidden' }"
			src="https://gist.githubusercontent.com/galinickel/0d4c25d095ac84150414c6c5507969bc/raw/1efd1187d4adda5a6fd223bec2ee2902ac20784e/loader-dots.svg"
			/>
			{{ text }}
		</p>
	</button>
</template>

<script>
export default {
	props: {
		text: String,
		isLoading: Boolean,
		color: String
	},
	data() {
		return {
			loading: this.isLoading
		}
	},
	methods: {

	}
}
</script>

<style>
@import url("https://cdn.d.greeninvoice.co.il/assets/web-app/2.2.331/components/webfonts/all.min.css");
.my-button {
	height: 56px;
	width: 228px;
	border-radius: 100px;
	border: none;
	cursor: pointer;
	font-family: "almoni-neue-dl", sans-serif;
}
.my-button p {
	color: #ffffff;
	font-size: 18px;
	font-weight: bold;
	letter-spacing: 0;
	line-height: 20px;
	text-align: center;
	display: flex;
	justify-content: space-evenly;
	width: 35%;
	align-items: center;
	margin: auto;
	padding-right: 25px;
}

.my-button img {
	width: 25px;
}
</style>