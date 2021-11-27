<script>
	export let name;
	export let tal1;
	export let tal2;
	export let correctSum;

	export let correct = false;
	export let wrong = false;

	export let timesTapped = 0;

	let endRoundTimeout = null;

	let initRound = () => {
		correct = false;
		wrong = false;

		tal1 = Math.ceil(Math.random() * 8);
		tal2 = Math.ceil(Math.random() * 7);

		correctSum = tal1+tal2;
		timesTapped= 0
	}


	window.addEventListener('load', initRound);

	let endRound = () => {
		correct = timesTapped === correctSum
		wrong = !correct;

		// initRound()
	}
	
	let handleClick = () => {
		clearTimeout(endRoundTimeout);
		endRoundTimeout = null;

		timesTapped++
		
		endRoundTimeout = setTimeout(() => {
			endRound();
		}, 5000);
	}

</script>

<main>
  <div class="container">
    <div class="tal">{tal1}</div>
    <div class="tal">+</div>
    <div class="tal">{tal2}</div>
  </div>
  <div>
    <div class="tapped">
      <button class:correct class:wrong on:animationend={initRound} on:click={handleClick}
        >{timesTapped}</button
      >
    </div>
  </div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  .tal,
  .tapped {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  button.wrong {
    background-color: rgb(206, 102, 102);
    animation: blink-animation 4s;
  }

  button.correct {
    background-color: rgb(153, 218, 57);
    animation: blink-animation 4s;
  }

  @keyframes blink-animation {
    0% {
		/* background-color: unset; */
    }
	20% {
		background-color: unset;
	}
    30% {
		background-color: inherit;
    }
	60% {
		/* background-color: white; */
	}
  }

  .container {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
