<!-- <script>
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";

  const progress = tweened(0, {
    duration: 400,
    easing: cubicOut,
  });
</script>

<progress value={$progress} />

<button on:click={() => progress.set(0)}> 0% </button>

<button on:click={() => progress.set(0.25)}> 25% </button>

<button on:click={() => progress.set(0.5)}> 50% </button>

<button on:click={() => progress.set(0.75)}> 75% </button>

<button on:click={() => progress.set(1)}> 100% </button>

<style>
  progress {
    display: block;
    width: 100%;
  }
</style> -->

<script>
  import { spring } from "svelte/motion";

  let coords = spring(
    { x: 50, y: 50 },
    {
      stiffness: 0.1,
      damping: 0.25,
    }
  );

  let size = spring(10);
</script>

<svg
  on:mousemove={(e) => {
    coords.set({ x: e.clientX, y: e.clientY });
  }}
  on:mousedown={() => size.set(30)}
  on:mouseup={() => size.set(10)}
>
  <circle cx={$coords.x} cy={$coords.y} r={$size} />
</svg>

<div class="controls">
  <label>
    <h3>stiffness ({coords.stiffness})</h3>
    <input
      bind:value={coords.stiffness}
      type="range"
      min="0.01"
      max="1"
      step="0.01"
    />
  </label>

  <label>
    <h3>damping ({coords.damping})</h3>
    <input
      bind:value={coords.damping}
      type="range"
      min="0.01"
      max="1"
      step="0.01"
    />
  </label>
</div>

<style>
  svg {
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
  }

  circle {
    fill: #ff3e00;
  }

  .controls {
    position: absolute;
    top: 1em;
    right: 1em;
    width: 200px;
    user-select: none;
  }

  .controls input {
    width: 100%;
  }
</style>
