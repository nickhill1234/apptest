<script>

	import { formatPriceForDisplay } from '@lib/formatters'


	export let price;

	let previousPrice = price;

	let priceElem, t;

	function onPriceChange(p) {
		if (!priceElem) return;
		p = formatPriceForDisplay(p) * 1;
		clearTimeout(t);
		priceElem.classList.remove('green');
		priceElem.classList.remove('red');
		if (p * 1 > previousPrice) {
			priceElem.classList.add('green');
		} else if (p * 1 < previousPrice) {
			priceElem.classList.add('red');
		}
		t = setTimeout(() => {
			if (!priceElem) return;
			priceElem.classList.remove('green');
			priceElem.classList.remove('red');
		}, 1000);
		previousPrice = p;
	}

	$: onPriceChange(price);

</script>

<style>

	.price {

	}

</style>

<span class='price' bind:this={priceElem}>
	{formatPriceForDisplay(price) || ''}
</span>