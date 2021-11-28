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

		tal1 = Math.floor(Math.random() * 9) + 1;
		tal2 = Math.floor(Math.random() * 9) + 1;

		correctSum = tal1+tal2;
		timesTapped= 0
	}


	window.addEventListener('load', initRound);

	let endRound = () => {
		correct = timesTapped === correctSum
		wrong = !correct;

		// initRound()
	}

	const pause = () => {
		setTimeout(()=> {
			initRound()
		}, 2000)

	}

	let handleClick = () => {
		clearTimeout(endRoundTimeout);
		endRoundTimeout = null;

		timesTapped++
		
		endRoundTimeout = setTimeout(() => {
			endRound();
		}, 2000);
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
      <button class:correct class:wrong on:animationend={pause} on:click={handleClick}
        >{timesTapped}</button
      >
    </div>
</div>
</main>

<style>
  main {
    text-align: center;
    width: 100%;
	height: 100%;
	display: flex;
	flex-direction: column;
	justify-content: space-around;
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
    animation: blink-animation 1s;
	color: white
  }

  button.correct {
    background-color: rgb(153, 218, 57);
    animation: blink-animation 1s;
  }

  @keyframes blink-animation {
    from {
		background-color: inherit;
		color: black
	}
	to {
		
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
