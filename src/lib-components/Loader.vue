<template>
	<div
		class="loader-dimmer"
		:style="{ visibility: isLoading ? 'visible' : 'hidden', opacity: isLoading? 1 : 0 }"
	>
		<img src="https://gist.githubusercontent.com/galinickel/0d4c25d095ac84150414c6c5507969bc/raw/1efd1187d4adda5a6fd223bec2ee2902ac20784e/loader-dots.svg" />
	</div>
</template>

<script>
export default {
	props: { isLoading: Boolean }
}
</script>

<style>
.loader-dimmer {
	transition: all 0.3s ease;
	background-color: rgba(0, 0, 0, 0.308);
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	left: 0;
	display: flex;
    align-items: center;
    justify-content: center;
}
.loader-dimmer img{
	width: 50px;
}
</style>