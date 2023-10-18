<script>
  let visible = false;

  function typewriter(node, { speed = 1 }) {
    const valid =
      node.childNodes.length === 1 &&
      node.childNodes[0].nodeType === Node.TEXT_NODE;

    if (!valid) {
      throw new Error(
        `This transition only works on elements with a single text node child`
      );
    }

    const text = node.textContent;
    const duration = text.length / (speed * 0.01);

    return {
      duration,
      tick: (t) => {
        const i = Math.trunc(text.length * t);
        node.textContent = text.slice(0, i);
      },
    };
  }
</script>

<label>
  <input type="checkbox" bind:checked={visible} />
  visible
</label>

{#if visible}
  <p transition:typewriter>The quick brown fox jumps over the lazy dog</p>
{/if}

<!-- 
<script>
	import { fly } from 'svelte/transition';

	let visible = true;
	let status = 'waiting...';
</script>

<p>status: {status}</p>

<label>
	<input type="checkbox" bind:checked={visible} />
	visible
</label>

{#if visible}
	<p
		transition:fly={{ y: 200, duration: 2000 }}
		on:introstart={() => status = 'intro started'}
		on:outrostart={() => status = 'outro started'}
		on:introend={() => status = 'intro ended'}
		on:outroend={() => status = 'outro ended'}
	>
		Flies in and out
	</p>
{/if} -->

<!-- 
<script>
	import { slide } from 'svelte/transition';

	let showItems = true;
	let i = 5;
	let items = ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine', 'ten'];
</script>

<label>
	<input type="checkbox" bind:checked={showItems} />
	show list
</label>

<label>
	<input type="range" bind:value={i} max="10" />
</label>

{#if showItems}
	{#each items.slice(0, i) as item}
		<div transition:slide|global>
			{item}
		</div>
	{/each}
{/if}

<style>
	div {
		padding: 0.5em 0;
		border-top: 1px solid #eee;
	}
</style> -->
