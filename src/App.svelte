<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'

  import { onMount } from 'svelte';
	import Knapsack from './components/Knapsack.svelte';
	import LCS from './components/LCS.svelte';
	import MinPathSum from './components/MinPathSum.svelte';
	import ClimbingStairs from './components/ClimbingStairs.svelte';
	let showMenu = false;
	let showScrollIndicator = true;
  
	function handleScroll() {
	  showMenu = window.scrollY > 200;
	  showScrollIndicator = window.scrollY < 100;
	}
  
	onMount(() => {
		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});
</script>


<main>
	<h1>Programarea Dinamică</h1>
	<p class="description">Rezolvarea problemelor prin tehnici avansate.</p>
  
	{#if showScrollIndicator}
	  <div class="scroll-indicator">Scroll</div>
	{/if}
  </main>
  
  {#if showMenu}
	<nav class="scroll-menu">
	  <a href="#knapsack">Problema Rucsacului</a>
	  <a href="#lcs">Subșirul Comun Maxim</a>
	  <a href="#minpath">Drumul Minim</a>
	  <a href="#stairs">Problema Scărilor</a>
	</nav>
  {/if}
  
  <section id="knapsack">
	<Knapsack explanation="Această problemă se poate rezolva utilizând o matrice pentru a memora valorile maxime pentru fiecare combinație de greutate și obiecte." />
  </section>
  <section id="lcs">
	<LCS />
  </section>
  <section id="minpath">
	<MinPathSum />
  </section>
  <section id="stairs">
	<ClimbingStairs />
  </section>
  
  <style>
	/* Stiluri pentru fundal și text */
	:global(body) {
	  margin: 0;
	  padding: 0;
	  box-sizing: border-box;
	  overflow-x: hidden;
	  font-family: 'Palatino', 'Palatino Linotype', 'Book Antiqua', serif;
	  background: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), url("/img/sky.jpg");
	  background-size: cover;
	  background-position: center;
	  background-attachment: fixed;
	  background-repeat: no-repeat;
	}
  
	main {
	  width: 100vw;
	  height: 100vh;
	  display: flex;
	  flex-direction: column;
	  justify-content: center;
	  text-align: center;
	  color: white;
	  position: relative;
	}
  
	h1 {
	  color: #ffffff;
	  text-transform: uppercase;
	  font-size: 4em;
	  font-weight: 100;
	  margin-bottom: 0.5em;
	  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
	}
  
	.description {
	  font-size: 1.2em;
	  margin-top: 1em;
	  color: #dddddd;
	  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
	}
  
	.scroll-indicator {
	  position: absolute;
	  bottom: 2em;
	  left: 50%;
	  transform: translateX(-50%);
	  width: 60px;
	  height: 60px;
	  background-color: rgba(255, 255, 255, 0.8);
	  border-radius: 50%;
	  display: flex;
	  align-items: center;
	  justify-content: center;
	  color: #000000;
	  font-size: 1em;
	  font-weight: bold;
	  animation: bounce 1.5s infinite;
	  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
	}
  
	@keyframes bounce {
	  0%, 100% { transform: translateX(-50%) translateY(0); }
	  50% { transform: translateX(-50%) translateY(-10px); }
	}
  
	.scroll-menu {
	  position: fixed;
	  top: 0;
	  width: 100%;
	  background-color: rgba(0, 0, 0, 0.8);
	  color: white;
	  display: flex;
	  justify-content: center;
	  gap: 20px;
	  padding: 1em 0;
	  z-index: 1000;
	  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
	}
  
	.scroll-menu a {
	  color: white;
	  text-decoration: none;
	  font-size: 1.1em;
	  font-weight: bold;
	  text-transform: uppercase;
	  transition: color 0.3s;
	}
  
	.scroll-menu a:hover {
	  color: #ff8c00;
	}
  
	section {
	  padding: 4em 2em;
	  margin-top: 4em;
	}
  
	section h2 {
	  font-size: 2.5em;
	  color: #fff;
	  text-transform: uppercase;
	  margin-bottom: 1em;
	}
  </style>




<!-- 
<main>
  <div>
    <a href="https://vite.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style> -->
