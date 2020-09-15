<template>
	<div class="grid-item joke-item">
		<div v-if="data.type==='single'">
			<p class="joke-content">{{data.joke}}</p>
		</div>
		<div v-else>
			<p class="setup-content">{{data.setup}}</p>
			<p class="delivery-content">{{data.delivery}}</p>
		</div>
	</div>
</template>

<script>
	export default {
		name: "CategoryItem",
		props: ["data"],
	};
</script>

<style lang="scss">
	@mixin paragraph($lines, $width) {
		display: -webkit-box;
		max-width: $width;
		-webkit-line-clamp: $lines;
		-webkit-box-orient: vertical;
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.joke-item {
		.joke-content {
			@include paragraph(6, 286px);
		}
		.setup-content {
			@include paragraph(3, 286px);
		}
		.delivery-content {
			@include paragraph(2, 286px);
			filter: blur(3px);
		}

		@media (max-width: 768px) {
			.joke-content {
				@include paragraph(6, 240px);
				text-align: center;
			}
			.setup-content {
				@include paragraph(3, 240px);
				text-align: center;
			}
			.delivery-content {
				@include paragraph(2, 240px);
				text-align: center;
			}
		}
	}
</style>