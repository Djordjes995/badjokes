<template>
	<ul class="main-nav">
		<li class="home-nav">BAD JOKES</li>
	</ul>
</template>

<script>
	export default {
		name: "Nav",
	};
</script>

<style lang="scss">
	@keyframes underline {
		from {
			left: 50%;
			right: 50%;
		}
		to {
			left: 1rem;
			right: 1rem;
		}
	}

	.main-nav {
		width: 100%;
		margin: 0;
		padding: 0;
		color: #fff;
		background-color: #000;
		font-weight: 500;
		list-style: none;
		display: flex;
		justify-content: center;
		li {
			padding: 1rem 2rem;
			cursor: pointer;
			transition: 0.2s all;
			position: relative;
			&:hover {
				&::after {
					content: "";
					position: absolute;
					bottom: 0;
					height: 0.2rem;
					background-color: #fff;
					animation: underline 0.25s;
					animation-fill-mode: forwards;
				}
			}
		}
		.home-nav {
			font-size: 1.5rem;
		}
	}
</style>