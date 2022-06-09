<script>
	let dingen = [
		{ vnaam: 'Peter', anaam: 'Felis', id: 1, pos: 1 },
		{ vnaam: 'Max', anaam: 'Felis', id: 2, pos: 2 },
		{ vnaam: 'Petry', anaam: 'Botter', id: 3, pos: 3 },
		{ vnaam: 'Stefanie', anaam: 'Felis', id: 4, pos: 4 },
		{ vnaam: 'Liv', anaam: 'Botter', id: 5, pos: 5 }
	];

	function drag(e) {
		const scherm = document.querySelectorAll('.lijst .card');
		for (let teller = 0; teller < scherm.length; teller++)
			dingen[teller].pos = scherm[teller].offsetTop;
	}

	function dragend(e) {
		let pos = e.clientY;
		let id = e.target.getAttribute('data-id');
		let aanpassen = dingen.findIndex((item) => item.id == id);
		dingen[aanpassen].pos = pos;
		dingen.sort((a, b) => a.pos - b.pos);
		for (let teller = 0; teller < dingen.length; teller++) dingen[teller].pos = teller + 1;
		console.log(dingen);
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
