<script>
	export let name;
	export let tal1;
	export let tal2;
	export let correctSum;

	export let correct = false;
	export let wrong = false;
	export let animateProgress = false;
	export let timesTapped = 0;

	export let statistics = []

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

		statistics.push({
			tal1,
			tal2,
			correct
		})

		// initRound()
	}

	const onEndAnimateProgress = () => {
		animateProgress = false
		// initRound()
	}

	const pause = () => {
		setTimeout(()=> {
			initRound()
		}, 2000)

	}

	let add = (addition) => {
		return () => {
			animateProgress = false
			clearTimeout(endRoundTimeout);
			endRoundTimeout = null;
			timesTapped += addition

			window.requestAnimationFrame(() => {
				animateProgress = true
				endRoundTimeout = setTimeout(() => {
				endRound();
			}, 2000);
			})
		}
	}

</script>

<main>
  <div class="container">
    <div class="tal">{tal1}</div>
    <div class="tal">+</div>
    <div class="tal">{tal2}</div>
  </div>
  <div class="progress" class:idle={timesTapped === 0}>
	{#if animateProgress}
	<div class="animate_progress" on:animationend={onEndAnimateProgress} />
	{/if}
  </div>
  <div>
    <div class="tapped">
      <button class:correct class:wrong on:animationend={pause} on:click={add(-1)}
        >-</button
      >
	  <div class="tapped-value">{timesTapped === 0 ? '?' : timesTapped}</div>
      <button class:correct class:wrong on:animationend={pause} on:click={add(1)}
        >+</button
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
    /* color: #ff3e00; */
    text-transform: uppercase;
    font-size: 10em;
    font-weight: 100;
  }

  .tapped {
	  display: flex;
	  align-items: center;
	  justify-content: space-evenly;
  }

  .tapped-value {
	  /* margin: 0 .1em; */
  }

  .progress {
	  border: 2px solid;
	  height: 2em;
	  border-radius: 8px;
	  margin: 0 18px
  }

  .filler {
	  width: 0%
  }

  .idle {
	background-color:lightgoldenrodyellow;
  }

  button {
	  animation: pulsate 1s infinite;
	  background-color: white;
	  border-radius: 8px;
	  border: 2px solid;
	  padding: 0;
	  margin: 0 18px;
	  width: 100%;
	  font-size: .6em;
	  touch-action: manipulation;
  }

  .animate_progress {
	animation: animate_progress 2s linear;
	background-color: greenyellow;
	height: 100%
	
  }

  @keyframes animate_progress {
	from {
		width: 0%;
	}
	to {
		width: 100%;
	}
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

  @keyframes pulsate {
	  50% {
		  background-color:lightgoldenrodyellow;
	  }
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
