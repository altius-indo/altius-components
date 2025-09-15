<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { cn } from '$lib/utils.js';
  export let href: string | undefined = undefined;
  export let active = false;
  export let disabled = false;
  export let className: string | undefined = undefined;
  const dispatch = createEventDispatcher<{ click: MouseEvent }>();
  function handleClick(event: MouseEvent) {
    if (disabled) {
      event.preventDefault();
      return;
    }
    dispatch('click', event);
  }
</script>

<a
  class={cn(
    'flex items-center gap-2 rounded px-3 py-2 text-sm transition-colors hover:bg-accent hover:text-accent-foreground',
    active && 'bg-accent text-accent-foreground',
    disabled && 'pointer-events-none opacity-50',
    className
  )}
  {href}
  aria-current={active ? 'page' : undefined}
  aria-disabled={disabled}
  on:click={handleClick}
>
  <slot name="left" />
  <slot />
  <slot name="right" />
</a>
