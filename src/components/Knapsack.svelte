<script>
  let tasks = [];
  let dependencies = [];
  let newTask = { name: "", duration: 0 };
  let newDependency = { from: "", to: "" };
  let result = { path: [], duration: 0 };

  const addTask = () => {
    if (newTask.name.trim() && newTask.duration > 0 && !tasks.some(t => t.name === newTask.name)) {
      tasks = [...tasks, { ...newTask }];
      newTask = { name: "", duration: 0 };
    } else {
      alert("Task invalid sau deja existent!");
    }
  };

  const addDependency = () => {
    if (
      newDependency.from && newDependency.to &&
      newDependency.from !== newDependency.to &&
      dependencies.every(dep => dep.from !== newDependency.from || dep.to !== newDependency.to)
    ) {
      dependencies = [...dependencies, { ...newDependency }];
      newDependency = { from: "", to: "" };
    } else {
      alert("Dependență invalidă sau duplicat!");
    }
  };

  const findCriticalPath = () => {
    if (tasks.length === 0) {
      alert("Adaugă activități înainte de a calcula drumul critic!");
      return;
    }

    // Inițializare structuri
    let adj = {}, durations = {}, inDegree = {}, earliest = {}, latest = {};
    
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

    // Sortare topologică (Kahn's Algorithm)
    let queue = Object.keys(inDegree).filter(k => inDegree[k] === 0);
    let topOrder = [];
    
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

    // Calculăm timpul cel mai devreme
    topOrder.forEach(task => {
      adj[task].forEach(neigh => {
        earliest[neigh] = Math.max(earliest[neigh] || 0, earliest[task] + durations[task]);
      });
    });

    // Durata totală a proiectului = maximul din earliest + durata ultimei activități
    let projectDuration = Math.max(...Object.values(earliest)) + durations[topOrder[topOrder.length - 1]];

    // Inițializare latest
    topOrder.reverse().forEach(task => latest[task] = projectDuration - durations[task]);

    // Calculăm timpul cel mai târziu
    topOrder.forEach(task => {
      adj[task].forEach(neigh => {
        latest[task] = Math.min(latest[task], latest[neigh] - durations[task]);
      });
    });

    // Găsim drumul critic
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
  <h1>Drumul Critic (CPM)</h1>

  <h2>Adaugă Activități</h2>
  <input type="text" bind:value={newTask.name} placeholder="Numele Activității" />
  <input type="number" bind:value={newTask.duration} min="1" />
  <button on:click={addTask}>Adaugă</button>

  <ul>{#each tasks as task} <li>{task.name} ({task.duration} zile)</li> {/each}</ul>

  <h2>Adaugă Dependențe</h2>
  <select bind:value={newDependency.from}>
    <option value="" disabled selected>De la...</option>
    {#each tasks as task} <option value={task.name}>{task.name}</option> {/each}
  </select>
  <select bind:value={newDependency.to}>
    <option value="" disabled selected>Către...</option>
    {#each tasks as task} <option value={task.name}>{task.name}</option> {/each}
  </select>
  <button on:click={addDependency}>Adaugă Dependență</button>

  <ul>{#each dependencies as dep} <li>{dep.from} → {dep.to}</li> {/each}</ul>

  <h2>Calculează Drumul Critic</h2>
  <button on:click={findCriticalPath}>Calculează</button>
  <button on:click={reset}>Resetează</button>

  {#if result.path.length > 0}
    <h3>Drumul Critic:</h3>
    <p>{result.path.join(" → ")}</p>
    <p>Durata totală: {result.duration} zile</p>
  {/if}
</main>

<style>
  main {
    background-color: #181818;
    color: #4CAF50;
    padding: 20px;
    border-radius: 8px;
  }

  input, select, button {
    margin-bottom: 10px;
    padding: 8px;
    border-radius: 4px;
    border: 1px solid #4CAF50;
    background-color: #282828;
    color: white;
  }

  button {
    background-color: #4CAF50;
    cursor: pointer;
    transition: 0.3s;
  }
  button:hover { background-color: #45a049; }
  ul { list-style: none; padding: 0; }
  li { margin-bottom: 5px; }
</style>