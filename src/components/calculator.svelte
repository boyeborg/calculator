<script lang="ts">
	const operandAtoms = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "."];
	const operators = ["+", "-", "/", "*"];

	type Calculator = {
		operand1: string | undefined;
		operator: string | undefined;
		operand2: string | undefined;
	};

	let calculator: Calculator = {
		operand1: undefined,
		operator: undefined,
		operand2: undefined,
	};

	function reset() {
		calculator = {
			operand1: undefined,
			operator: undefined,
			operand2: undefined,
		};
	}

	function addOperandAtom(
		operandAtom: string,
		operand: "operand1" | "operand2"
	) {
		if (!calculator[operand]) {
			calculator[operand] = operandAtom;
			return;
		}
		if (calculator[operand].includes(".") && operandAtom === ".") return; // Cannot have more than one comma
		if (calculator[operand] === "" && operandAtom === ".") {
			calculator[operand] = "0.";
		} else {
			calculator[operand] += operandAtom;
		}
	}

	function onClick(event: Event & { currentTarget: HTMLButtonElement }) {
		const input = event.currentTarget.textContent;

		if (input === "C") {
			reset();
		} else if (input === "E") {
			const { operand1, operand2 } = calculator;
			if (!operand2) {
				calculator.operand1 = String(Math.pow(10, Number(operand1)));
			} else {
				calculator.operand2 = String(Math.pow(10, Number(operand2)));
			}
		} else if (input === "=") {
			if (calculator.operand1 && calculator.operand2 && calculator.operator) {
				const { operand1, operator, operand2 } = calculator;
				const result = String(eval(`${operand1} ${operator} ${operand2}`));
				calculator = {
					operand1: result,
					operator: undefined,
					operand2: undefined,
				};
			}
		} else if (!calculator.operator) {
			if (operandAtoms.includes(input)) {
				addOperandAtom(input, "operand1");
			} else if (calculator.operand1 && operators.includes(input)) {
				calculator.operator = input;
			}
		} else {
			if (operandAtoms.includes(input)) {
				addOperandAtom(input, "operand2");
			} else if (operators.includes(input)) {
				const { operand1, operator, operand2 } = calculator;
				if (operand2) {
					const result = String(eval(`${operand1} ${operator} ${operand2}`));
					calculator = {
						operand1: result,
						operator: input,
						operand2: undefined,
					};
				}
				calculator.operator = input;
			}
		}
	}

	let display = "";

	$: {
		if (calculator.operand2) {
			display = calculator.operand2;
		} else {
			display = calculator.operand1 || "";
		}
	}
</script>

<section>
	<header>Calculator</header>
	<form on:submit|preventDefault={() => {}}>
		<span style="grid-area: display">{display}</span>

		<!-- Clear -->
		<button style="grid-area: clear" on:click={onClick}>C</button>

		<!-- Numbers -->
		<button class="num-0" style="grid-area: num-0" on:click={onClick}>0</button>
		<button style="grid-area: num-1" on:click={onClick}>1</button>
		<button style="grid-area: num-2" on:click={onClick}>2</button>
		<button style="grid-area: num-3" on:click={onClick}>3</button>
		<button style="grid-area: num-4" on:click={onClick}>4</button>
		<button style="grid-area: num-5" on:click={onClick}>5</button>
		<button style="grid-area: num-6" on:click={onClick}>6</button>
		<button style="grid-area: num-7" on:click={onClick}>7</button>
		<button style="grid-area: num-8" on:click={onClick}>8</button>
		<button style="grid-area: num-9" on:click={onClick}>9</button>

		<!-- Comma -->
		<button style="grid-area: comma" on:click={onClick}>.</button>

		<!-- Operators -->
		<button class="plus" style="grid-area: plus" on:click={onClick}>+</button>
		<button style="grid-area: minus" on:click={onClick}>-</button>
		<button style="grid-area: multiply" on:click={onClick}>*</button>
		<button style="grid-area: divide" on:click={onClick}>/</button>
		<button style="grid-area: exponent" on:click={onClick}>E</button>
		<button type="submit" style="grid-area: equal" on:click={onClick}>=</button>
	</form>
</section>

<style>
	section {
		display: inline-block;
		font-family: monospace;
		background: black;
		border: 2px solid black;
		border-radius: 10px;
		padding: 0 5px 5px 0;
		width: 13rem;
	}

	header {
		font-weight: 600;
		font-size: 1.2rem;
		background: white;
		border-radius: 10px 10px 0 0;
		color: black;
		padding: 0.2em 0.8rem;
		display: flex;
		justify-content: flex-end;
		align-items: center;
	}

	form {
		display: grid;
		grid-template-areas:
			"display display display display"
			"clear exponent equal multiply"
			"num-7 num-8 num-9 divide"
			"num-4 num-5 num-6 minus"
			"num-3 num-2 num-1 plus"
			"num-0 num-0 comma plus";
		gap: 0.5rem;
		padding: 0.8rem;
		background-color: white;
		background-image: radial-gradient(
			circle at 1px 1px,
			black 1px,
			transparent 0
		);
		background-size: 4px 4px;
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
		overflow: hidden;
		padding-right: 0.2rem;
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

	button.plus {
		height: auto;
	}

	button.num-0 {
		width: auto;
	}
</style>
