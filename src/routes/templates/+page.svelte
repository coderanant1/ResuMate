<script lang="ts">
  import { onMount } from "svelte";
  import Default from "$lib/templates/default.svelte";
  import Minimal from "$lib/templates/minimal.svelte";
  import Tile from "$lib/templates/tile.svelte";

  let List = [
    { name: "default", component: Default },
    { name: "minimal", component: Minimal },
    { name: "tile", component: Tile },
  ];

  onMount(() => document.body.style.overflow = "visible");
</script>

<div class="flex flex-wrap gap-8 justify-center p-4 sm:p-8 lg:p-10">
  {#each List as x}
    <div
      style="scale: 0.3"
      class="!origin-top-left grid gap-3 w-[63mm] min-h-[89.1mm] h-full md:scale-50 lg:scale-30"
    >
      <a
        class="badge text-primary-fg w-full text-3xl sm:text-5xl h-fit p-5 justify-center capitalize"
        href="/?theme={x.name}"
      >{x.name}</a>

      <div class="doc">
        <x.component />
      </div>
    </div>
  {/each}
</div>
