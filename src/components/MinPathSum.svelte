<script>
	let minPathSumCode = `
#include <iostream>
using namespace std;

int minPathSum(int grid[][100], int m, int n) {
    int dp[100][100];
    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; i++) dp[i][0] = dp[i - 1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j - 1] + grid[0][j];

    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = grid[i][j] + min(dp[i - 1][j], dp[i][j - 1]);
        }
    }
    return dp[m - 1][n - 1];
}

int main() {
    int m, n;
    cin >> m >> n;
    int grid[100][100];
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }
    cout << minPathSum(grid, m, n) << endl;
    return 0;
}`;
</script>

<section id="minpath">
	<h2 class="problem-title">3. Problema Drumului Minim (Minimum Path Sum)</h2>
	<div class="explanation">
		<p>Această problemă constă în găsirea unei căi de cost minim de la colțul din stânga sus al unei matrice la colțul din dreapta jos, utilizând doar deplasări către dreapta și în jos.</p>
	</div>
	<div class="code-container">
		<pre><code>{minPathSumCode}</code></pre>
	</div>
</section>

<style>
	/* Stiluri generale */
	.problem-title {
		font-size: 2em;
		color: #ffffff;
		text-transform: uppercase;
		margin-bottom: 1em;
		text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
		padding: 0.2em 0.5em;
		background-color: rgba(0, 0, 0, 0.5);
		border-radius: 8px;
		display: inline-block;
	}

	.explanation {
		color: #dddddd;
		font-size: 1.2em;
		margin-bottom: 1em;
		text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
	}

	.code-container {
		background-color: rgba(0, 0, 0, 0.8);
		color: #00ff00; /* Culoare asemănătoare pentru cod */
		padding: 1em;
		border-radius: 8px;
		box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.5);
		overflow-x: auto;
	}

	pre {
		margin: 0;
		font-family: 'Courier New', Courier, monospace;
		font-size: 1em;
		line-height: 1.5;
		white-space: pre-wrap; /* Pentru a permite wrap-ul textului */
		word-wrap: break-word;
	}

	code {
		font-family: 'Courier New', Courier, monospace;
		color: #00ff00; /* Culoare specifică codului */
	}
</style>
