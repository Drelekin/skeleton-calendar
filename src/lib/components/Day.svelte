<script lang="ts">
	export let date: number = 0;
	export let background: string = '';
</script>

<button
	on:click
	class="bg-cover rounded-container-token"
	style="background-image: url({background});"
>
	<h3 class="p-4 text-lg drop-shadow md:text-xl xl:text-2xl 2xl:text-4xl">{date}</h3>
</button>
