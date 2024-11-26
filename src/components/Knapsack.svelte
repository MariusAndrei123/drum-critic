<script>
    let knapsackCppCode = `
#include <iostream>
using namespace std;

int main() {
    int n, maxWeight;
    cout << "Introduceți numărul de obiecte: ";
    cin >> n;

    cout << "Introduceți greutatea maximă permisă: ";
    cin >> maxWeight;

    int weight[100], value[100];
    for (int i = 0; i < n; i++) {
        cout << "Introduceți greutatea și valoarea pentru obiectul " << i + 1 << ": ";
        cin >> weight[i] >> value[i];
    }

    int dp[101][101] = {0};

    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= maxWeight; w++) {
            if (weight[i - 1] <= w) {
                dp[i][w] = max(dp[i - 1][w], dp[i - 1][w - weight[i - 1]] + value[i - 1]);
            } else {
                dp[i][w] = dp[i - 1][w];
            }
        }
    }

    cout << "Valoarea maximă obținută este: " << dp[n][maxWeight] << endl;

    cout << "Obiectele selectate sunt: ";
    int w = maxWeight;
    for (int i = n; i > 0 && w > 0; i--) {
        if (dp[i][w] != dp[i - 1][w]) {
            cout << i << " ";
            w -= weight[i - 1];
        }
    }

    cout << endl;

    return 0;
}`;
    let items = [];
    let maxWeight = 0;
    let currentItem = { name: "", weight: 0, value: 0 };
  
    const addItem = () => {
      currentItem.weight = parseFloat(currentItem.weight);
      currentItem.value = parseInt(currentItem.value, 10);
  
      if (
        currentItem.name.trim() &&
        !isNaN(currentItem.weight) &&
        currentItem.weight > 0 &&
        !isNaN(currentItem.value) &&
        currentItem.value > 0
      ) {
        items = [...items, { ...currentItem }];
        currentItem = { name: "", weight: 0, value: 0 };
      } else {
        alert("Completează toate câmpurile corect!");
      }
    };
  
    const knapsack = () => {
      maxWeight = parseInt(maxWeight, 10);
      if (isNaN(maxWeight) || maxWeight <= 0) {
        alert("Introduceți o greutate maximă validă!");
        return { value: 0, items: [] };
      }
  
      const n = items.length;
      const dp = Array(n + 1)
        .fill()
        .map(() => Array(maxWeight + 1).fill(0));
  
      for (let i = 1; i <= n; i++) {
        for (let w = 1; w <= maxWeight; w++) {
          if (items[i - 1].weight <= w) {
            dp[i][w] = Math.max(
              items[i - 1].value + dp[i - 1][w - items[i - 1].weight],
              dp[i - 1][w]
            );
          } else {
            dp[i][w] = dp[i - 1][w];
          }
        }
      }
  
      let w = maxWeight;
      let selectedItems = [];
      for (let i = n; i > 0 && w > 0; i--) {
        if (dp[i][w] !== dp[i - 1][w]) {
          selectedItems.push(items[i - 1]);
          w -= items[i - 1].weight;
        }
      }
  
      return { value: dp[n][maxWeight], items: selectedItems };
    };
  
    const reset = () => {
      items = [];
      maxWeight = 0;
      currentItem = { name: "", weight: 0, value: 0 };
      result = { value: 0, items: [] };
    };
  
    let result = { value: 0, items: [] };
  </script>
  
  <main class="interactive-exercise">
    <h1>1. Exercițiu Problema Rucsacului</h1>
  
    <p>
      Imaginează-ți că ești un călător și trebuie să îți împachetezi un rucsac
      cu cele mai valoroase obiecte, fără a depăși limita de greutate. Fiecare obiect
      are o greutate (în kilograme) și o valoare. Sarcina ta este să maximizezi valoarea totală
      a obiectelor din rucsac, menținând greutatea totală sub limita dată.
    </p>
  
    <p><strong>Explicații:</strong></p>
    <ul>
      <li><strong>Valoarea unui obiect</strong>: Reprezintă importanța sau prețul obiectului. De exemplu, un obiect de valoare mai mare poate fi mai important în funcție de utilitatea sa.</li>
      <li><strong>Greutatea unui obiect</strong>: Este măsurată în kilograme și reprezintă cât de greu este obiectul. De exemplu, un obiect mai greu va ocupa mai mult spațiu în rucsac.</li>
    </ul>
  
    <div class="input-section">
      <label for="maxWeight">Greutatea maximă (kg):</label>
      <input id="maxWeight" type="number" bind:value={maxWeight} min="1" />
  
      <h2>Adaugă un obiect</h2>
      <label for="name">Numele obiectului:</label>
      <input id="name" type="text" bind:value={currentItem.name} />
  
      <label for="weight">Greutatea obiectului (kg):</label>
      <input id="weight" type="number" bind:value={currentItem.weight} min="0.1" step="0.1" />
  
      <label for="value">Valoarea obiectului:</label>
      <input id="value" type="number" bind:value={currentItem.value} min="1" />
  
      <button on:click={addItem}>Adaugă obiect</button>
    </div>
  
    <div class="items-list">
      <h3>Obiecte în rucsac:</h3>
      <ul>
        {#each items as item}
          <li>{item.name} - Greutate: {item.weight} kg, Valoare: {item.value}</li>
        {/each}
      </ul>
    </div>
  
    <button on:click={() => result = knapsack()}>Calculează soluția optimă</button>
  
    <button on:click={reset}>Resetează</button>
  
    {#if result.items.length > 0}
      <div class="result">
        <h3>Soluția optimă a problemei rucsacului:</h3>
        <p>Valoare totală: {result.value}</p>
        <ul>
          {#each result.items as item}
            <li>{item.name} - Greutate: {item.weight} kg, Valoare: {item.value}</li>
          {/each}
        </ul>
      </div>
    {/if}
    <div class="code-container">
      <h2>Cod C++ explicat pentru problema rucsacului:</h2>
      <pre><code>{knapsackCppCode}</code></pre>
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
  
    .items-list {
      margin-top: 20px;
      margin-bottom: 20px;
    }
  
    .result {
      margin-top: 20px;
      padding: 10px;
      background-color: #333;
      border-radius: 8px;
    }
  
    ul {
      list-style-type: none;
      padding: 0;
    }
  
    li {
      margin-bottom: 5px;
    }
  
    p {
      font-size: 18px;
      margin-bottom: 20px;
    }
  </style>
  