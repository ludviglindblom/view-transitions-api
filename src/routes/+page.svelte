<script>
	import frank from '$lib/videos/frank-fam_reel.mp4';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="View Transitions API demo app" />
</svelte:head>

<section>
	<h1>View Transitions API</h1>
	<div class="frank">
		<!-- svelte-ignore a11y-media-has-caption -->
		<video src={frank} muted autoplay loop playsinline></video>
	</div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.frank {
		display: block;
		position: relative;
		width: 100%;
		aspect-ratio: 16/9;
	}

	.frank video {
		position: absolute;
		width: 100%;
		height: 100%;
	}
</style>
