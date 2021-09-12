<section>
	<header>Calculator</header>
	<form>
		<span style="grid-area: display">3</span>

		<!-- Order buttons for accassibility -->

		<!-- Clear -->
		<button style="grid-area: clear">C</button>

		<!-- Numbers -->
		<button class="num-0" style="grid-area: num-0">0</button>
		<button style="grid-area: num-1">1</button>
		<button style="grid-area: num-2">2</button>
		<button style="grid-area: num-3">3</button>
		<button style="grid-area: num-4">4</button>
		<button style="grid-area: num-5">5</button>
		<button style="grid-area: num-6">6</button>
		<button style="grid-area: num-7">7</button>
		<button style="grid-area: num-8">8</button>
		<button style="grid-area: num-9">9</button>

		<!-- Comma -->
		<button style="grid-area: comma">.</button>

		<!-- Operators -->
		<button style="grid-area: plus">+</button>
		<button style="grid-area: minus">-</button>
		<button style="grid-area: multiply">*</button>
		<button style="grid-area: divide">/</button>
		<button style="grid-area: equal-1">=</button>
		<!-- Why are there two equal signs, Steve? Why? -->
		<button class="equal-2" style="grid-area: equal-2">=</button>
	</form>
</section>

<style>
	section {
		display: inline-block;
		font-family: monospace;
		background: black;
		border-radius: 10px;
		padding: 0 5px 5px 0;
	}

	header {
		font-weight: 600;
		font-size: 1.2rem;
		color: white;
		padding: 0.2em;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	header::before {
		content: "";
		display: inline-block;
		width: 0.8rem;
		height: 0.8rem;
		border: 0.1rem solid white;
		border-radius: 1px;
		margin-right: 10px;
	}

	form {
		display: grid;
		grid-template-areas:
			"display display display display"
			"clear equal-1 divide multiply"
			"num-7 num-8 num-9 minus"
			"num-4 num-5 num-6 plus"
			"num-3 num-2 num-1 equal-2"
			"num-0 num-0 comma equal-2";
		gap: 0.5rem;
		padding: 0.8rem;
		background: lightgray;
		border-radius: 10px;
		border: 0.1rem solid black;
	}

	span {
		display: flex;
		align-items: center;
		justify-content: flex-end;
		font-family: monospace;
		background: white;
		text-align: right;
		font-size: 1rem;
		line-height: 1;
		border: 0.1rem solid black;
		border-radius: 1px;
		height: 2rem;
		margin: 0;
		padding: 0;
	}

	button {
		font-family: monospace;
		font-size: 1rem;
		border: 0.1rem solid black;
		border-radius: 1px;
		background: white;
		box-shadow: 0.2rem 0.2rem 0 0 black;
		padding: 0;
		margin: 0;
		width: 2.3rem;
		height: 2.3rem;
		cursor: pointer;
	}

	button.equal-2 {
		height: auto;
	}

	button.num-0 {
		width: auto;
	}
</style>
