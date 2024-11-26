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
  
  <main class="interactive-exercise">
	<h1>3. Problema Drumului Minim (Minimum Path Sum)</h1>
  
	<p>
	  Această problemă constă în găsirea unei căi de cost minim de la colțul din stânga sus al unei
	  matrice la colțul din dreapta jos, utilizând doar deplasări către dreapta și în jos. 
	  Este o problemă clasică de programare dinamică.
	</p>
  
	<p><strong>Explicații:</strong></p>
	<ul>
	  <li><strong>Intrare:</strong> O matrice de dimensiuni m x n cu costuri pentru fiecare celulă.</li>
	  <li><strong>Ieșire:</strong> Costul minim pentru a ajunge în colțul din dreapta jos.</li>
	</ul>
	<br><br/>
	<h2>Cod C++ pentru drumul minim:</h2>
	<div class="code-container">
	  <pre><code>{minPathSumCode}</code></pre>
	</div>
  </main>
  
  <style>
	.interactive-exercise {
	  background-color: #181818;
	  color: #4CAF50;
	  padding: 20px;
	  border-radius: 8px;
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
  