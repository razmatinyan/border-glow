<template>
	<div class="cards" @mousemove="onMousemove">
		<div v-for="i in props.count" class="card">
			<div class="card-content">
				<h2>{{ i }}</h2>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
interface Props {
	count?: number;
}

const props = withDefaults(defineProps<Props>(), {
	count: 16,
});

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
.cards {
	display: grid;
	grid-template-columns: repeat(4, 150px);
	grid-template-rows: repeat(4, 150px);
	gap: 8px;
	padding: 32px;
}

.card :is(h2) {
	opacity: 0.45;
	transition: 0.2s;
}

.card:hover :is(h2) {
	opacity: 1;
}

.card-content {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	gap: 16px;
	background: #13161c;
	border-radius: inherit;
	transition: all 0.2s;
	height: calc(100% - 2px);
	width: calc(100% - 2px);
}

.cards,
.card:hover::before {
	opacity: 1;
}

.cards:hover .card {
	background: radial-gradient(
		800px circle at var(--xPos) var(--yPos),
		rgba(0, 255, 241, 0.4),
		transparent 15%
	);
}

.card {
	position: relative;
	display: flex;
	justify-content: center;
	align-items: center;
	background: radial-gradient(400px circle at 0 0, rgba(0, 255, 241, 0), transparent 0%);
	border-radius: 8px;
	transition: 0.1s;
}

.card::before {
	content: '';
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	border-radius: inherit;
	background: radial-gradient(
		500px circle at var(--xPos) var(--yPos),
		rgba(0, 255, 241, 0.1),
		transparent 35%
	);
	opacity: 0;
	transition: all 0.15s ease-in-out;
}
</style>
