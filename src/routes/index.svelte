<script>

	let lala = [];

	let dingen = [
		{ vnaam: 'Peter', anaam: 'Felis', id: 1, pos: 100 },
		{ vnaam: 'Max', anaam: 'Felis', id: 2, pos: 200 },
		{ vnaam: 'Petry', anaam: 'Botter', id: 3, pos: 300 },
		{ vnaam: 'Stefanie', anaam: 'Felis', id: 4, pos: 400 },
		{ vnaam: 'Liv', anaam: 'Botter', id: 5, pos: 500 }
	];

	function drag(e) {
		let hulp=[];
		let scherm = document.querySelectorAll('.lijst .card');
		scherm.forEach((item) => {
			hulp.push({ y: item.offsetTop, id: item.getAttribute('data-id') });
		});
		lala=[...hulp];
		
	}

	function dragend(e) {
		let pos = e.clientY;
		let id = e.target.getAttribute('data-id');

		let teverwijderen = lala.findIndex((item) => item.id ==id )
		let intevoegen = (lala.splice(teverwijderen,1));
		let nieuwedingen=[];

		
		for (let teller = 0; teller<=lala.length; teller++) {
			if (pos < lala[teller].y) {
				lala.splice(teller,0,intevoegen[0]);
				break;				
			}
		}
		
		
		for (let teller=0; teller<lala.length; teller++){
	 	nieuwedingen.push(dingen[lala[teller].id-1]);	
		}			
		console.log(nieuwedingen);

		//console.log(dingen);
		//console.log(intevoegen);
		//let nieuwdingen = [...dingen];
		dingen=[];
		dingen = nieuwedingen;
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
