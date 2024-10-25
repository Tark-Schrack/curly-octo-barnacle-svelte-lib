<script lang="ts">
  import type { EventHandler } from "svelte/elements";

  let {
    value = $bindable("text"),
    type = "text",
    oninput,
    ...stuff
  }: { value: any; type: string; oninput: EventHandler } = $props();
</script>

<div class="container">
  <span class="text">
    {value}
  </span>
  <input {type} class="input" bind:value {...stuff} {oninput} />
</div>

<style>
  .container {
    display: inline-block;
    position: relative;
  }
  .input,
  .text {
    margin: 0;
    padding: 2px 10px;
    height: var(--height, var(--font-size, auto));
    width: var(--width, auto);
    font-family: var(--font-family, "Fira Sans", sans-serif);
    font-size: var(--font-size, 1rem);
    line-height: var(--font-size, 1rem);
    min-width: var(--min-width, 5ch);
  }
  .text {
    padding-right: 2ch;
    display: inline-block;
    visibility: hidden;
    white-space: pre;
  }
  .input {
    text-align: center;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
  }
</style>
