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

    document.getElementById('result').innerHTML = `
      <p>Lungimea subșirului comun maxim este: ${dp[m][n]}</p>
    `;
  }
</script>

<main class="interactive-exercise">
  <h1>2. Exercițiu LCS (Longest Common Subsequence)</h1>

  <p>
    Problema constă în găsirea celui mai lung subșir comun (LCS) între două șiruri de caractere date.
    Aceasta este folosită adesea în bioinformatică, procesare de texte sau comparații de date.
  </p>

  <p><strong>Explicații:</strong></p>
  <ul>
    <li><strong>Șirul X:</strong> Primul șir de caractere pe care îl analizăm.</li>
    <li><strong>Șirul Y:</strong> Al doilea șir de caractere.</li>
  </ul>

  <div class="input-section">
    <label for="stringX">Șirul X:</label>
    <input id="stringX" type="text" placeholder="Ex: ABCD" />

    <label for="stringY">Șirul Y:</label>
    <input id="stringY" type="text" placeholder="Ex: ABD" />

    <button on:click={calculateLCS}>Calculează LCS</button>
  </div>

  <div class="result" id="result"></div>

  <h2>Cod C++ pentru LCS:</h2>
  <div class="code-container">
    <pre><code>{lcsCode}</code></pre>
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
