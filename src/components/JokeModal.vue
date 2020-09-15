<template>
	<transition name="modal">
		<div class="modal-mask">
			<div class="modal-wrapper">
				<div class="modal-container">
					<div class="modal-header joke-header">
						<div class="header">
							<h3>The joke</h3>
						</div>
					</div>
					<div class="modal-body">
						<slot name="body"></slot>
					</div>
					<div class="modal-footer joke-footer">
						<slot name="footer">
							<button class="primary" @click="$emit('close')">Yay</button>
							<button @click="$emit('close')">Nay</button>
						</slot>
					</div>
				</div>
			</div>
		</div>
	</transition>
</template>

<script>
	export default {
		name: "JokeModal",
	};
</script>

<style lang="scss">
	.modal-mask {
		position: fixed;
		z-index: 9998;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.5);
		display: table;
		transition: opacity 0.3s ease;
	}

	.modal-wrapper {
		display: table-cell;
		vertical-align: middle;
	}

	.modal-container {
		width: 600px;
		margin: 0px auto;
		padding: 20px 30px;
		background-color: #fff;
		border-radius: 2px;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
		transition: all 0.3s ease;
	}

	.modal-header.joke-header {
		justify-content: center;
		border-color: #f2f2f2;
		padding-top: 0;
		h3 {
			margin-top: 0;
			font-weight: 500;
			text-transform: uppercase;
		}
	}

	.modal-body {
		margin: 20px 0;
		font-size: 1.2rem;
		p {
			overflow-wrap: break-word;
		}
	}

	.modal-default-button {
		float: right;
	}

	.modal-enter {
		opacity: 0;
	}

	.modal-leave-active {
		opacity: 0;
	}

	.modal-footer.joke-footer {
		justify-content: center;
		border-color: #f2f2f2;
		button {
			font-weight: 500;
			padding: 0.25rem 2.5rem;
			text-transform: uppercase;
			margin: 0.5rem 1rem;
			font-size: 14px;
			border: 2px solid #000;
			background-color: #fff;
			color: #000;
			transition: 0.2s all;
			border-radius: 2px;
			&.primary {
				background-color: #000;
				color: #fff;
			}
			&:hover {
				background-color: #ff4647;
				border: 2px solid #ff4647;
				color: #fff;
			}
		}
	}

	.modal-enter .modal-container,
	.modal-leave-active .modal-container {
		-webkit-transform: scale(1.1);
		transform: scale(1.1);
	}

	@media (max-width: 768px) {
		.modal-container {
			width: 100%;
			height: 100%;
		}
		.modal-body {
			overflow-y: auto;
			p {
				overflow-wrap: anywhere;
				font-size: 1rem;
			}
		}
		.modal-footer.joke-footer {
			position: absolute;
			bottom: 0;
			left: 0;
			right: 0;
			button {
				margin: 0.5rem;
			}
		}
	}
</style>