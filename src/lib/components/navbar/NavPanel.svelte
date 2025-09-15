<script lang="ts">
  import { createEventDispatcher, onMount, onDestroy } from 'svelte';
  import { fly } from 'svelte/transition';
  export let open = false;
  const dispatch = createEventDispatcher();
  function close() {
    dispatch('close');
  }
  function handleKey(e: KeyboardEvent) {
    if (e.key === 'Escape') {
      close();
    }
  }
  onMount(() => document.addEventListener('keydown', handleKey));
  onDestroy(() => document.removeEventListener('keydown', handleKey));
</script>

{#if open}
<div class="fixed inset-0 z-40">
  <button
    type="button"
    class="absolute inset-0 bg-black/50"
    aria-label="Close navigation panel"
    on:click={close}
  ></button>
  <nav
    in:fly={{ x: -320 }}
    out:fly={{ x: -320 }}
    class="relative h-full w-full max-w-xs bg-background p-4 overflow-y-auto sm:w-80"
  >
    <slot />
  </nav>
</div>
{/if}
