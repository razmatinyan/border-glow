<template>
	<main>
		<Cards />
	</main>
</template>

<script setup lang="ts">
const onMousemove = (event: MouseEvent) => {
	const cards = document.querySelectorAll<HTMLElement>('.card');
	cards.forEach((card) => {
		const rect = card.getBoundingClientRect();

		const x = event.clientX - rect.left;
		const y = event.clientY - rect.top;

		card.style.setProperty('--xPos', `${x}px`);
		card.style.setProperty('--yPos', `${y}px`);
	});
};
</script>

<style>
*,
*::before,
*::after {
	margin: 0;
	padding: 0;
	font-family: 'JetBrains Mono';
	box-sizing: border-box;
}
body {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 100vh;
	background: #0c1016;
	color: #fff;
}
</style>
