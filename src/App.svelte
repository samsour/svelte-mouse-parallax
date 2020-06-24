<script>
	let width;
	let height;

	const cursor = { x: width / 2, y: height / 2 };
	const modifier = 50 // less = more movement

	$: distanceX = width / 2 - cursor.x;
	$: distanceY =  height / 2 - cursor.y;

	const layers = [
		{
			url: "https://s3-us-west-2.amazonaws.com/s.cdpn.io/272781/ilu_bg.jpg",
			align: "left",
		},
		{
			url: "https://s3-us-west-2.amazonaws.com/s.cdpn.io/272781/ilu_03.png",
			align: "left",
		},
		{
			url: "https://s3-us-west-2.amazonaws.com/s.cdpn.io/272781/ilu_02.png",
			align: "left",
		},
		{
			url: "https://s3-us-west-2.amazonaws.com/s.cdpn.io/272781/ilu_man.png",
			align: "right",
		},
		{
			url: "https://s3-us-west-2.amazonaws.com/s.cdpn.io/272781/ilu_01.png",
			align: "left",
		},
		{
			url: "https://s3-us-west-2.amazonaws.com/s.cdpn.io/272781/ilu_overlay.png",
			align: "left",
		},
	]

	function handleMousemove(event) {
		cursor.x = event.clientX;
		cursor.y = event.clientY;
	}
</script>

<svelte:window bind:innerHeight={height} bind:innerWidth="{width}"/>

<div class="parallax-container" on:mousemove={handleMousemove}>
	{#each layers as layer, index}
		<img
			style="transform: translate({distanceX * (index + 1) / modifier}px,{distanceY * (index + 1) / modifier}px); {layer.align == "left" ? 'left:0' : 'right:0'}"
			src="{layer.url}"
			alt="parallax layer {index}"
		>
	{/each}
	<div
		class="parallax layer text"
		style="transform: translate({distanceX * 3 / modifier}px,{distanceY * 3 / modifier}px)"
	>
		Fancy Parallax Text
	</div>
</div>

<style>
.parallax-container {
	position: fixed;
	width: 110vw;
	height: 110vh;
	left: 50%;
	transform: translate(-50%, 0);
}

.parallax-container img {
	position: absolute;
	bottom: 0;
	right: 0;
	object-fit: cover;
	will-change: transform;
}

.text {
	width: 100%;
	height: 100%;
	display: flex;
	align-items: center;
	justify-content: center;
}

:global(body) {
	margin: 0;
	padding: 0;
	background-color: rgb(231, 231, 231);
}
</style>