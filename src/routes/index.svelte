<script>
	import { draggable } from '@neodrag/svelte';
	import { each, loop_guard } from 'svelte/internal';

	let hulp = [];

	let dingen = [
		{ vnaam: 'Peter', anaam: 'Felis', id: 1, pos: 100 },
		{ vnaam: 'Max', anaam: 'Felis', id: 2, pos: 200 },
		{ vnaam: 'Petry', anaam: 'Botter', id: 3, pos: 300 },
		{ vnaam: 'Stefanie', anaam: 'Felis', id: 4, pos: 400 },
		{ vnaam: 'Liv', anaam: 'Botter', id: 5, pos: 500 }
	];

	function drag(e) {
		let scherm = document.querySelectorAll('.lijst .card');
		scherm.forEach((item) => {
			hulp.push({ y: item.offsetTop, id: item.getAttribute('data-id') });
		});
	}

	function dragend(e) {
		let pos = e.clientY;
		console.log('pos ' + pos);
		let id = e.target.getAttribute('data-id');
		let intevoegen = dingen.filter((dingen) => dingen.id == id);
		let nieuwedingen = [];

		console.log(hulp.length);
		for (let teller = 0; teller < hulp.length - 1; teller++) {
			console.log(teller);
			console.log(pos < hulp[teller].y);
			if (pos > hulp[teller].y) {
				console.log('bier ' + teller);
				nieuwedingen.push(hulp[teller]);
			} else {
				nieuwedingen.push({ y: pos, id: id });
				break;
			}
		}
		console.log(nieuwedingen);
		dingen = dingen.filter((dingen) => dingen.id != id);

		//console.log(dingen);
		//console.log(intevoegen);
		//let nieuwdingen = [...dingen];
		//dingen = nieuwdingen;
	}
</script>

<div class="lijst">
	{#each dingen as ding}
		<div
			data-id={ding.id}
			class="card"
			draggable="true"
			on:dragstart={(e) => drag(e)}
			on:dragend={(e) => dragend(e)}
		>
			{ding.vnaam} - {ding.anaam}
		</div>
	{/each}
</div>

<style>
	.raar {
		background-color: aqua;
		color: red;
	}
	.card {
		border: 1px solid black;
		border-radius: 4px;
		padding: 8px;
		margin-top: 5px;
	}

	.lijst {
		width: 40%;
	}
</style>
