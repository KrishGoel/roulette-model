<script>
	// Total numbers on mat = 36 + 2 (0, 00) [American, cuz Vegas lmao]
	// Payout for "straigh-up" = 35x

	function randomInteger(max) {
		return Math.floor(Math.random() * max);
	}

	// Parameters
	const iterations = 38
	const totalOutcomes = 38 // {1, 2, 3, .... 35, 36, 0, 00}
	const maxBet = 1
	const minBet = 5

	function round() {
		let winner = randomInteger(totalOutcomes) + 1 // To ensure the winner's not 0
	
		let totalInvestment = 0
		let investment = []
		for (let i = 0; i < totalOutcomes; i++) {
			let bet = randomInteger(maxBet - minBet) + minBet
			investment.push(bet)
			totalInvestment += bet
		}
	
		let reward = investment[winner] * 35
	
		let result = reward - totalInvestment

		return [winner, totalInvestment, reward, result]
	}
	// console.log(round())

	// Final data
	let winners = []
	let totalInvestments = []
	let rewards = []
	let results = []

	for (let i = 0; i < iterations; i++) {
		winners.push(round()[0])
		totalInvestments.push(round()[1])
		rewards.push(round()[2])
		results.push(round()[3])
	}

	let balance = 0
	for (let j = 0; j < iterations; j++) {
		balance += results[j]
	}
</script>

<main>
	<h1>Roulette Experiment</h1>
	<table>
		<tr>
			<th>Iteration</th>
			<th>Winner</th>
			<th>Total Investment</th>
			<th>Reward</th>
			<th>Balance</th>
		</tr>
		{#each winners as entry, i}
		<tr>
			<td>{i}</td>
			<td>{winners[i]}</td>
			<td>{totalInvestments[i]}</td>
			<td>{rewards[i]}</td>
			<td>{results[i]}</td>
		</tr>
		{/each}
	</table>
	<h2>{balance}</h2>
</main>