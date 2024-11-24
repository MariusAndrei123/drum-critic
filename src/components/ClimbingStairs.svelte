<script>
	let climbStairsCode = `
#include <iostream>
using namespace std;

int climbStairs(int n) {
    if (n == 1) return 1;
    if (n == 2) return 2;

    int dp[101] = {0};
    dp[1] = 1;
    dp[2] = 2;

    for (int i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}

int main() {
    int n;
    cin >> n;
    cout << climbStairs(n) << endl;
    return 0;
}`;
</script>

<h2 class="problem-title">4. Problema Scărilor (Climbing Stairs)</h2>
<div class="code-container">
	<pre><code>{climbStairsCode}</code></pre>
</div>

<style>
	.problem-title {
		font-size: 2.5em;
		color: #ffffff;
		text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
		margin-bottom: 1em;
		padding: 0.2em 0.5em;
		background-color: rgba(0, 0, 0, 0.5);
		border-radius: 8px;
		display: inline-block;
	}

	.code-container {
		position: relative;
		background-color: rgba(255, 255, 255, 0.8);
		padding: 1.5em;
		border-radius: 8px;
		margin-top: 1em;
		box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
	}

	.code-container::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(255, 255, 255, 0.7);
		filter: blur(8px);
		z-index: -1;
	}
</style>
Z