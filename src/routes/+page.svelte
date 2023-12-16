<script lang="ts">
	import { onMount } from 'svelte';
	import Day from '$lib/components/Day.svelte';

	const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
	const months = [
		'January',
		'February',
		'March',
		'April',
		'May',
		'June',
		'July',
		'August',
		'September',
		'October',
		'November',
		'December'
	];

	let background: string = 'https://picsum.photos/id/237/1920/1080';

	let now: Date = new Date();
	let currentMonth: string;
	let currentYear: number;
	let currentDate: number;
	let currentDay: string;
	let currentTime: string;

	onMount(() => {
		const interval = setInterval(() => {
			now = new Date();
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});

	$: {
		currentMonth = months[now.getMonth()];
		currentYear = now.getFullYear();
		currentDate = now.getDate();
		currentDay = days[now.getDay()];
		currentTime = `${now.getHours()}:${now.getMinutes().toString().padStart(2, '0')}:${now
			.getSeconds()
			.toString()
			.padStart(2, '0')}`;
	}

	const backgrounds = Array.from(
		{ length: 30 },
		(_, i) => `https://picsum.photos/id/${10 + i}/600/600`
	);
</script>

<div class="flex h-full flex-col p-4 lg:p-8">
	<div class="flex justify-between">
		<h2 class="text-xl drop-shadow md:text-2xl lg:text-3xl xl:text-4xl 2xl:text-5xl">
			{currentDay}, {currentMonth}
			{currentDate}, {currentYear}
		</h2>
		<h2 class="text-xl drop-shadow md:text-2xl lg:text-3xl xl:text-4xl 2xl:text-5xl">
			{currentTime}
		</h2>
	</div>

	<div class="mb-2 mt-4 grid grid-cols-7 gap-2 lg:mb-4 lg:mt-8 lg:gap-4">
		{#each days as day}
			<div
				class="overflow-hidden bg-surface-500 p-2 text-center font-light drop-shadow backdrop-blur rounded-container-token md:text-lg xl:text-xl"
			>
				{day}
			</div>
		{/each}
	</div>

	<div class="grid flex-1 grid-cols-7 gap-2 lg:gap-4">
		{#each Array(30) as _, i (i)}
			<Day date={i + 1} background={backgrounds[i]} />
		{/each}
	</div>
</div>
