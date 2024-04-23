<script>
	import { onMount } from 'svelte';
	import { onNavigate } from '$app/navigation';
	import Header from './Header.svelte';
	import './styles.css';

	let x = 0;
	let y = 0;
	let endRadius = 0;

	onMount(() => {
		document.body.addEventListener('click', (e) => {
			x = innerWidth / 2;
			y = innerHeight / 2;
			endRadius = Math.hypot(Math.max(x, innerWidth - x), Math.max(y, innerHeight - y));
		});
	});

	onNavigate((navigation) => {
		if (document.startViewTransition) return;

		return new Promise((resolve) => {
			let transition = document.startViewTransition(async () => {
				resolve();
				await navigation.complete;
			});

			transition.ready.then(() => {
				// Animate the root’s new view
				/* document.documentElement.animate(
					{
						clipPath: [`circle(0 at ${x}px ${y}px)`, `circle(${endRadius}px at ${x}px ${y}px)`]
					},
					{
						duration: 500,
						easing: 'ease-in',
						// Specify which pseudo-element to animate
						pseudoElement: '::view-transition-new(root)'
					}
				); */
			});
		});
	});
</script>

<div class="app">
	<Header />

	<main>
		<slot />
	</main>

	<footer>
		<p>visit <a href="https://frankfam.co">frankfam.co</a></p>
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}

	/* @keyframes fade-in {
		from {
			opacity: 0;
		}
	}

	@keyframes fade-out {
		to {
			opacity: 0;
		}
	}

	@keyframes slide-from-right {
		from {
			transform: translateX(50%);
		}
	}

	@keyframes slide-to-left {
		to {
			transform: translateX(-50%);
		}
	}

	:root::view-transition-old(root) {
		animation:
			90ms cubic-bezier(0.4, 0, 1, 1) both fade-out,
			300ms cubic-bezier(0.4, 0, 0.2, 1) both slide-to-left;
	}

	:root::view-transition-new(root) {
		animation:
			210ms cubic-bezier(0, 0, 0.2, 1) 90ms both fade-in,
			300ms cubic-bezier(0.4, 0, 0.2, 1) both slide-from-right;
	} */

	/* ::view-transition-old(root),
	::view-transition-new(root) {
		animation: none;
		mix-blend-mode: normal;
		display: block;
	} */
</style>
