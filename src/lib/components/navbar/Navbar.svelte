<script lang="ts">
  import NavPanel from './NavPanel.svelte';
  import NavItem from './NavItem.svelte';
  import Button from '$lib/components/ui/button/button.svelte';
  let panelOpen = false;
  let userMenuOpen = false;
  let loggedIn = false;
  function togglePanel() {
    panelOpen = !panelOpen;
  }
  function closePanel() {
    panelOpen = false;
  }
  function toggleUserMenu() {
    userMenuOpen = !userMenuOpen;
  }
  function logOut() {
    loggedIn = false;
    userMenuOpen = false;
  }
</script>

<div class="sticky top-0 z-50 w-full border-b bg-background">
  <div class="relative flex h-14 items-center justify-between px-4">
    <button
      class="mr-2 rounded p-2 focus:outline-none focus:ring"
      aria-label="Open navigation"
      on:click={togglePanel}
    >
      &#9776;
    </button>
    <a href="/" class="absolute left-1/2 -translate-x-1/2 text-lg font-bold">Altius</a>
    <div class="flex items-center gap-2">
      {#if loggedIn}
        <div class="relative">
          <button
            class="flex h-8 w-8 items-center justify-center rounded-full bg-accent text-accent-foreground"
            aria-haspopup="menu"
            aria-expanded={userMenuOpen}
            on:click={toggleUserMenu}
          >
            U
          </button>
          {#if userMenuOpen}
            <div class="absolute right-0 mt-2 w-40 rounded-md border bg-popover p-2 text-sm shadow">
              <a class="block rounded px-2 py-1 hover:bg-accent hover:text-accent-foreground" href="/preferences">Preferences</a>
              <a class="block rounded px-2 py-1 hover:bg-accent hover:text-accent-foreground" href="/account">Account</a>
              <button class="block w-full rounded px-2 py-1 text-left hover:bg-accent hover:text-accent-foreground" on:click={logOut}>Log out</button>
            </div>
          {/if}
        </div>
      {:else}
        <Button on:click={() => (loggedIn = true)}>Log in</Button>
      {/if}
      <a href="/settings" aria-label="Settings" class="rounded p-2 hover:bg-accent hover:text-accent-foreground">&#8942;</a>
    </div>
  </div>
</div>

<NavPanel open={panelOpen} on:close={closePanel}>
  <NavItem href="/" active>Home</NavItem>
  <NavItem href="/about">About</NavItem>
</NavPanel>
