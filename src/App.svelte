<script>
	import drumCriticImage from './assets/img/drum_critic.png'; // Importă imaginea
  
	let tasks = [];
	let dependencies = [];
	let newTask = { name: "", duration: 0 };
	let newDependency = { from: "", to: "" };
	let result = { path: [], duration: 0 };
  
	// Adaugă un task nou
	const addTask = () => {
	  if (newTask.name.trim() && newTask.duration > 0 && !tasks.some(t => t.name === newTask.name)) {
		tasks = [...tasks, { ...newTask }];
		newTask = { name: "", duration: 0 };
	  } else {
		alert("Task invalid sau deja existent!");
	  }
	};
  
	// Adaugă o dependență între task-uri
	const addDependency = () => {
	  if (newDependency.from && newDependency.to && newDependency.from !== newDependency.to) {
		dependencies = [...dependencies, { ...newDependency }];
		newDependency = { from: "", to: "" };
	  } else {
		alert("Dependență invalidă!");
	  }
	};
  
	// Algoritmul pentru drumul critic (CPM)
	const findCriticalPath = () => {
	  if (tasks.length === 0 || dependencies.length === 0) {
		alert("Adaugă activități și dependențe înainte de a calcula drumul critic!");
		return;
	  }
  
	  let adj = {}, durations = {};
	  let earliest = {}, latest = {};
	  let inDegree = {}, topOrder = [];
  
	  tasks.forEach(({ name, duration }) => {
		adj[name] = [];
		durations[name] = duration;
		earliest[name] = 0;
		inDegree[name] = 0;
	  });
  
	  dependencies.forEach(({ from, to }) => {
		adj[from].push(to);
		inDegree[to] = (inDegree[to] || 0) + 1;
	  });
  
	  let queue = Object.keys(inDegree).filter(k => inDegree[k] === 0);
	  while (queue.length) {
		let node = queue.shift();
		topOrder.push(node);
		adj[node].forEach(neigh => {
		  inDegree[neigh]--;
		  if (inDegree[neigh] === 0) queue.push(neigh);
		});
	  }
  
	  if (topOrder.length !== tasks.length) {
		alert("Graf invalid! Verifică dependențele (cicluri sau date greșite).");
		return;
	  }
  
	  topOrder.forEach(task => {
		adj[task].forEach(neigh => {
		  earliest[neigh] = Math.max(earliest[neigh] || 0, earliest[task] + durations[task]);
		});
	  });
  
	  let projectDuration = Math.max(...Object.values(earliest)) + Math.max(...Object.values(durations));
  
	  topOrder.reverse().forEach(task => latest[task] = projectDuration - durations[task]);
	  topOrder.forEach(task => {
		adj[task].forEach(neigh => {
		  latest[task] = Math.min(latest[task], latest[neigh] - durations[task]);
		});
	  });
  
	  let criticalPath = topOrder.filter(task => earliest[task] === latest[task]);
  
	  result = { path: criticalPath, duration: projectDuration };
	};
  
	const reset = () => {
	  tasks = [];
	  dependencies = [];
	  result = { path: [], duration: 0 };
	};
  </script>
  
  <main>
	<h1>Drumul Critic (Critical Path Method)</h1>
  
	<section>
	  <h2>Ce este Drumul Critic?</h2>
	  <p>
		Metoda drumului critic (CPM) este utilizată pentru gestionarea proiectelor, ajutând la identificarea celor mai importante activități care determină durata totală a proiectului.
	  </p>
	  <p>
		Se folosește pentru a găsi activitățile care nu pot întârzia fără a afecta termenul final al proiectului.
	  </p>
	</section>
  
	<section>
	  <h2>Exemplu Vizual</h2>
	  <p>Diagrama de mai jos ilustrează un proiect cu mai multe activități și dependențele lor:</p>
	  <img src={drumCriticImage} alt="Imagine drum critic" style="max-width: 60%; height: auto;" />
	  <br><br/>
	  <br><br/>
	  <h2>Cum funcționează Drumul Critic?</h2>
	  <p>
		Drumul critic (Critical Path Method - CPM) este o tehnică utilizată în gestionarea proiectelor pentru a identifica cele mai importante activități care determină durata totală a proiectului.
	  </p>
	  <h3>Pași pentru identificarea drumului critic:</h3>
	  <ul>
		<li>1. Se identifică toate căile posibile de la început la sfârșit.</li>
		<li>2. Se calculează durata fiecărei căi.</li>
		<li>3. Drumul cu durata cea mai mare este drumul critic.</li>
	  </ul>
	  <p>
		În exemplul de mai sus, trebuie analizate toate traseele posibile și să se determine care dintre ele este cel mai lung. Acest traseu este cel care nu poate întârzia fără a afecta termenul limită al proiectului.
	  </p>
	</section>
  

	














	<section>
		<h2>Algoritm pentru Drumul Critic</h2>
		<p>
		  Mai jos este un exemplu de algoritm C++ care determină drumul critic într-un proiect.
		</p>
		<div class="code-container">
		  <pre class="code-block">
			{@html `
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;#include &lt;iostream&gt; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;using namespace std; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;const int NMAX = 20; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;const int INF = 1000000000; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;double la[NMAX][NMAX];  // Duratele arcelor (matrice de adiacență) 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;double t[NMAX], tb[NMAX]; // Timpul de început și finalizare 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;int n; 
			  
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;void citire() { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;for (int i = 0; i &lt; NMAX; i++) { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for (int j = 0; j &lt; NMAX; j++) { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;la[i][j] = -1; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;} 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;} 
			  <br><br>
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;cout &lt;&lt; "Introduceti arcele si duratele. Terminati cu 0 0 0:\\n"; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;while (true) { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int x, y; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;double c; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cout &lt;&lt; "Arc: "; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cin &gt;&gt; x &gt;&gt; y; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (x == 0 && y == 0) break; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cout &lt;&lt; "Durata: "; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cin &gt;&gt; c; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;la[x][y] = c; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;n = max(n, max(x, y)); 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;} 
			  <br>
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;int main() { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for (int i = 0; i &lt; NMAX; i++) { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;t[i] = -1; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tb[i] = -1; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;} 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;citire(); 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cout &lt;&lt; "EVENIMENTELE CRITICE SUNT: \\n"; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for (int i = 1; i &lt;= n; i++) { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (t[i] == tb[i]) { 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cout &lt;&lt; "Evenimentul " &lt;&lt; i &lt;&lt; endl; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;} 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;} 
			  <br><br>
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return 0; 
			  <br>&nbsp;&nbsp;&nbsp;&nbsp;} 
			  <br>
			`}
		  </pre>
		</div>
	  </section>
	  
	  
	 
	  
	  

















	  

  
	<section class="interactive-exercise">
	  <h2>Simulează Drumul Critic</h2>
  
	  <h3>Adaugă Activități</h3>
	  <input type="text" bind:value={newTask.name} placeholder="Numele Activității" />
	  <input type="number" bind:value={newTask.duration} placeholder="Durata" min="1" />
	  <button on:click={addTask}>Adaugă</button>
  
	  <ul>
		{#each tasks as task}
		  <li>{task.name} (Durată: {task.duration})</li>
		{/each}
	  </ul>
  
	  <h3>Adaugă Dependențe</h3>
	  <select bind:value={newDependency.from}>
		<option value="" disabled selected>De la...</option>
		{#each tasks as task}
		  <option value={task.name}>{task.name}</option>
		{/each}
	  </select>
  
	  <select bind:value={newDependency.to}>
		<option value="" disabled selected>Către...</option>
		{#each tasks as task}
		  <option value={task.name}>{task.name}</option>
		{/each}
	  </select>
  
	  <button on:click={addDependency}>Adaugă Dependență</button>
  
	  <ul>
		{#each dependencies as dep}
		  <li>{dep.from} → {dep.to}</li>
		{/each}
	  </ul>
  
	  <h3>Calculează Drumul Critic</h3>
	  <button on:click={findCriticalPath}>Calculează</button>
	  <button on:click={reset}>Resetează</button>
  
	  {#if result.path.length > 0}
		<h3>Drumul Critic:</h3>
		<p>{result.path.join(" → ")}</p>
		<p>Durata totală: {result.duration}</p>
	  {/if}
	</section>
  </main>

  <style>
	main {
	  font-family: Arial, sans-serif;
	  color: #4CAF50;
	  background-color: #181818;
	  padding: 20px;
	  border-radius: 8px;
	}
  
	section {
	  margin-bottom: 20px;
	  padding: 15px;
	  background-color: #282828;
	  border-radius: 8px;
	}
  
	input {
	  margin-bottom: 10px;
	  padding: 5px;
	  border-radius: 4px;
	  border: 1px solid #4CAF50;
	  background-color: #333;
	  color: #fff;
	}
  
	button {
	  background-color: #4CAF50;
	  color: white;
	  border: none;
	  padding: 10px;
	  border-radius: 4px;
	  cursor: pointer;
	}
  
	button:hover {
	  background-color: #45a049;
	}
  
	ul {
	  list-style-type: none;
	  padding: 0;
	}
  
	li {
	  margin-bottom: 5px;
	}
  </style>
  