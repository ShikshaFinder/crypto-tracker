<script>
	import CoinCard from "./CoinCard.svelte";
import coincard from "./CoinCard.svelte"
	let name = "crypto tracker"
 let coins = [];
async function fetchCoins() {
 const response = await fetch("https://api.coinstats.app/public/v1/coins?skip=0&limit=78");
 const data = await response.json();
 coins = data.coins;
 console.log("coins:", coins);
}
function changeIsPositive(priceChange) { 
  return priceChange >= 0;
}
</script>
<main>
	<h1> {name} !</h1>
	<button on:click={fetchCoins}>fetch data</button>
	<div class="grid">
	{#each coins as coin}
	<div class="coin-card">
  <img class="coin-image" src={coin.icon} alt={coin.name} />
  <p class="coin-name">{coin.name}</p>
  <div class="coin-details">
    <div
      class="detail-field price-change" class:positive={changeIsPositive(coin.priceChange1w)}
    >
      {coin.priceChange1w}%
    </div>
    <div class="detail-field">{coin.price.toFixed(2)}$</div>
    <a class="detail-field" href={coin.websiteUrl}>Website &#8594;</a>
  </div>
</div>
	{/each}
</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		background-color: black;
		color: blanchedalmond;
	}

	h1 {
		color: #fa561f;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}		
						  main {
    text-align: center;
    padding: 40px 0;
    margin: 0 auto;
  }
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
  }
@media (min-width: 640px) {
    main {
      max-width: 1600px;
      padding: 40px 20px;
    }
  }						
.positive {
    color: #16a34a;
}															
</style>