<script>
	let climbStairsCode = `
  #include <iostream>
  using namespace std;
  
  int climbStairs(int n) {
	  if (n == 1) return 1;
	  if (n == 2) return 2;
  
	  int dp[101] = {0};
	  dp[1] = 1;
	  dp[2] = 2;
  
	  for (int i = 3; i <= n; i++) {
		  dp[i] = dp[i - 1] + dp[i - 2];
	  }
	  return dp[n];
  }
  
  int main() {
	  int n;
	  cin >> n;
	  cout << climbStairs(n) << endl;
	  return 0;
  }`;

	let stairsInput = ''; // Legat de input-ul utilizatorului
	let result = ''; // Mesajul afișat în UI

	function calculateWays() {
		const n = parseInt(stairsInput); // Convertim inputul în număr
		if (isNaN(n) || n <= 0) {
			result = 'Vă rugăm să introduceți un număr pozitiv!';
			return;
		}

		// Algoritmul pentru Climbing Stairs
		let dp = Array(n + 1).fill(0);
		dp[1] = 1;
		if (n >= 2) dp[2] = 2;

		for (let i = 3; i <= n; i++) {
			dp[i] = dp[i - 1] + dp[i - 2];
		}

		// Actualizăm rezultatul
		result = `Numărul total de moduri de a urca ${n} trepte este: ${dp[n]}`;
	}
</script>

<main class="interactive-exercise">
	<h1>Problema Scărilor (Climbing Stairs)</h1>

	<p>
		Problema **Climbing Stairs** constă în determinarea numărului de moduri
		în care poți urca o scară de **n** trepte, având posibilitatea de a urca fie 1 treaptă, fie 2 trepte odată.
	</p>

	<div class="input-section">
		<label for="stairsInput">Numărul de trepte:</label>
		<input
			id="stairsInput"
			type="number"
			bind:value={stairsInput}
			placeholder="Ex: 5"
		/>

		<button on:click={calculateWays}>Calculează modurile</button>
	</div>

	<div class="result">
		{#if result}
			<p>{result}</p>
		{/if}
	</div>

	<h2>Cod C++ pentru Climbing Stairs:</h2>
	<div class="code-container">
		<pre><code>{climbStairsCode}</code></pre>
	</div>
</main>

<style>
	.interactive-exercise {
		background-color: #181818;
		color: #4CAF50;
		padding: 20px;
		border-radius: 8px;
	}

	.input-section {
		margin-bottom: 20px;
	}

	label {
		font-weight: bold;
		display: block;
	}

	input {
		margin-bottom: 10px;
		padding: 5px;
		border-radius: 4px;
		border: 1px solid #4CAF50;
		background-color: #282828;
		color: #fff;
		width: 100%;
	}

	button {
		background-color: #4CAF50;
		color: white;
		border: none;
		padding: 10px;
		border-radius: 4px;
		cursor: pointer;
		transition: background-color 0.3s;
	}

	button:hover {
		background-color: #45a049;
	}

	.result {
		margin-top: 20px;
		padding: 10px;
		background-color: #333;
		border-radius: 8px;
		color: #fff;
	}

	.code-container {
		background-color: #1a1a1a;
		color: #4CAF50;
		padding: 10px;
		border-radius: 8px;
		overflow-x: auto;
		margin-top: 20px;
	}

	pre {
		font-family: 'Courier New', Courier, monospace;
		font-size: 1em;
		white-space: pre-wrap;
		word-wrap: break-word;
		margin: 0;
	}

	code {
		color: #4CAF50;
	}
</style>
