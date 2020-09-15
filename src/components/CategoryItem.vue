<template>
	<div class="grid-item">
		<h3 class="category-title">{{data.name}}</h3>
		<p class="category-number">{{data.jokes.length}}</p>
	</div>
</template>

<script>
	export default {
		name: "CategoryItem",
		props: ["data"],
	};
</script>

<style lang="scss">
	.grid-item {
		border: 1px solid #f2f2f2;
		cursor: pointer;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 2rem;
		margin-bottom: 1.5rem;
		border-radius: 2px;
		transition: 0.2s all;
		height: 15rem;
		&:hover {
			box-shadow: 9px 8px 10px -9px rgba(140, 140, 140, 0.66);
			transform: scale(1.05);
		}
		.category-title {
			font-weight: 500;
			text-transform: uppercase;
		}
		.category-number {
			font-size: 1rem;
			font-weight: 500;
			font-size: 1.5rem;
			color: #fff;
			background: black;
			line-height: 1;
			padding: 5px 20px;
		}
	}
</style>