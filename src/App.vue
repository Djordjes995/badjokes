<template>
	<div id="app">
		<main-navigation></main-navigation>
		<main-content></main-content>
	</div>
</template>

<script>
	import MainNavigation from "./components/MainNavigation";
	import MainContent from "./components/MainContent";

	export default {
		name: "App",
		components: {
			MainNavigation,
			MainContent,
		},
	};
</script>

<style lang="scss">
	@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap");

	body {
		font-family: "Roboto", sans-serif;
		margin: 0;
		padding: 0;
		overflow-x: none;
	}
</style>
