<script>
    let lcsCode = `
  #include <iostream>
  #include <cstring>
  using namespace std;
  
  int lcs(const char X[], const char Y[]) {
      int m = strlen(X), n = strlen(Y);
      int dp[101][101] = {0};
      for (int i = 1; i <= m; i++) {
          for (int j = 1; j <= n; j++) {
              if (X[i - 1] == Y[j - 1])
                  dp[i][j] = dp[i - 1][j - 1] + 1;
              else
                  dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
          }
      }
      return dp[m][n];
  }
  
  int main() {
      char X[101], Y[101];
      cin >> X >> Y;
      cout << lcs(X, Y) << endl;
      return 0;
  }`;
  
    // Functie pentru calculul LCS in JavaScript
    function calculateLCS() {
      const X = document.getElementById('stringX').value;
      const Y = document.getElementById('stringY').value;
      
      let m = X.length, n = Y.length;
      let dp = Array.from(Array(m + 1), () => Array(n + 1).fill(0));
  
      for (let i = 1; i <= m; i++) {
        for (let j = 1; j <= n; j++) {
          if (X[i - 1] === Y[j - 1]) {
            dp[i][j] = dp[i - 1][j - 1] + 1;
          } else {
            dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
          }
        }
      }
  
      // Afișează lungimea LCS-ului
      document.getElementById('result').textContent = `Lungimea subșirului comun maxim este: ${dp[m][n]}`;
    }
  </script>
  
  <section id="lcs">
    <h2 class="problem-title">2. Problema Subșirului Comun Maxim (LCS)</h2>
    <div class="explanation">
      <p>Această problemă constă în găsirea lungimii celui mai lung subșir comun între două șiruri date.</p>
      <ul>
        <li><strong>Șirul X:</strong> Primul șir de caractere.</li>
        <li><strong>Șirul Y:</strong> Al doilea șir de caractere.</li>
      </ul>
    </div>
    <div class="code-container">
      <pre><code>{lcsCode}</code></pre>
    </div>
  
    <div class="input-section">
      <label for="stringX">Șirul X:</label>
      <input id="stringX" type="text" placeholder="Ex: ABCD" />
  
      <label for="stringY">Șirul Y:</label>
      <input id="stringY" type="text" placeholder="Ex: ABD" />
  
      <!-- Schimbă onclick cu on:click -->
      <button on:click={calculateLCS}>Calculează LCS</button>
    </div>
  
    <div class="result" id="result"></div>
  </section>
  
  <style>
    .problem-title {
      font-size: 2em;
      color: #ffffff;
      text-transform: uppercase;
      margin-bottom: 1em;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
      padding: 0.5em 1em;
      background-color: #4CAF50; /* Culoare similară cu stilul knapsack */
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
      background-color: #1a1a1a; /* Fond întunecat */
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
      white-space: pre-wrap;
      word-wrap: break-word;
    }
  
    code {
      font-family: 'Courier New', Courier, monospace;
      color: #00ff00;
    }
  
    .input-section {
      margin-top: 20px;
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
    }
  
    input:disabled {
      background-color: #3a3a3a;
      cursor: not-allowed;
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
  
    p {
      font-size: 18px;
      margin-bottom: 20px;
    }
  </style>
  