<script>
    let matrixChainOptimizationCode = `
  #include <iostream>
  using namespace std;
  
  const int INF = 1000000000; // Valoare mare pentru "infinit"
  
  int matrixChainOrder(int dims[], int n) {
      int dp[100][100]; // Matricea pentru stocarea costurilor minime
  
      // Inițializare: costul pentru o singură matrice este 0
      for (int i = 0; i < n; ++i) {
          for (int j = 0; j < n; ++j) {
              dp[i][j] = (i == j) ? 0 : INF;
          }
      }
  
      // Calculăm costurile pentru lanțuri de diferite lungimi
      for (int len = 2; len <= n; ++len) {
          for (int i = 0; i <= n - len; ++i) {
              int j = i + len - 1;
              for (int k = i; k < j; ++k) {
                  int cost = dp[i][k] + dp[k + 1][j] + dims[i] * dims[k + 1] * dims[j + 1];
                  dp[i][j] = min(dp[i][j], cost);
              }
          }
      }
  
      return dp[0][n - 1];
  }
  
  int main() {
      int dims[] = {10, 30, 5, 60}; // Dimensiunile matricilor
      int n = sizeof(dims) / sizeof(dims[0]) - 1; // Numărul de matrici
      cout << "Costul minim pentru înmulțirea matricilor este: " << matrixChainOrder(dims, n) << endl;
      return 0;
  }`;
  </script>
  
  <main class="interactive-exercise">
    <h1>5. Optimizarea Lanțului de Matrici (Matrix Chain Optimization)</h1>
  
    <p>
      Această problemă constă în determinarea ordinii optime pentru înmulțirea unui lanț de matrici,
      astfel încât costul total al înmulțirii să fie minim. Costul unei operații este definit ca
      produsul dimensiunilor matricilor implicate.
    </p>
  
    <p><strong>Explicații:</strong></p>
    <ul>
      <li><strong>Dimensiunile matricilor:</strong> Reprezintă șirul de dimensiuni asociate matricilor (ex. {10, 30, 5, 60}).</li>
      <li><strong>Costul minim:</strong> Costul cel mai mic pentru a înmulți toate matricile în ordine optimă.</li>
    </ul>
    <br><br/>
    <h2>Cod C++ pentru optimizare:</h2>

    <div class="code-container">
      <pre><code>{matrixChainOptimizationCode}</code></pre>
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
  