<script>
	import { onMount } from 'svelte';
	import Knapsack from './components/Knapsack.svelte';
	import LCS from './components/LCS.svelte';
	import MinPathSum from './components/MinPathSum.svelte';
	import ClimbingStairs from './components/ClimbingStairs.svelte';
	import Matrixop from './components/Matrixop.svelte';

	let showMenu = false;
	let showScrollIndicator = true;

	let text = `
Programarea dinamică este o tehnică de rezolvare a problemelor complexe, bazată pe împărțirea acestora în subprobleme mai mici, ușor de gestionat. Soluțiile fiecărei subprobleme sunt stocate pentru a evita recalculările, economisind astfel timp și resurse.

Această metodă este aplicabilă atunci când problema îndeplinește două proprietăți esențiale:
1. **Suprapunerea subproblemelor** – Aceleași subcalculuri apar în mod repetat.
2. **Structura optimă** – Soluția problemei principale poate fi construită din soluțiile subproblemelor.

Există două abordări principale:
- **Top-down**: Se folosește o funcție recursivă, iar rezultatele intermediare sunt memorate pentru utilizări ulterioare.
- **Bottom-up**: Problemele sunt rezolvate iterativ, pornind de la cele mai simple cazuri.

Programarea dinamică este utilizată pentru:
- Calcularea celui mai scurt drum (ex.: algoritmul lui Dijkstra);
- Rezolvarea problemei rucsacului (Knapsack);
- Parantezarea optimă a matricilor;
- Determinarea subșirurilor comune maxime (Longest Common Subsequence).

Această tehnică reduce complexitatea de la exponențială la polinomială în multe cazuri, făcând-o indispensabilă în optimizarea soluțiilor algoritmice.
`;

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

	<div class="text-container">
		<div class="text-content">
			{text}
		</div>
	</div>

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
	<a href="#matrix">Operații Matrice</a>
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
<section id="matrix">
	<Matrixop />
</section>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		overflow-x: hidden;
		font-family: 'Palatino', serif;
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
		justify-content: flex-start;  /* Aliniere verticală ajustată */
		align-items: center;  /* Centrare pe orizontală */
		text-align: center;
		color: white;
		position: relative;
		padding-top: 5em;  /* Spațiu mai mare de sus pentru titlu */
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

	.text-container {
		margin: 2em auto;
		width: 80%;
		background: rgba(255, 255, 255, 0.1);
		padding: 1.5em;
		border-radius: 10px;
		box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.5);
	}

	.text-content {
		color: #e0e0e0;
		line-height: 1.6;
		font-size: 1.1em;
		text-align: left;
		white-space: pre-wrap;
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
