<script lang="ts">
  import { onMount } from "svelte";
  import { page } from "$app/state";
  import { Btn, Tab, Tabs, TabsList } from "@haze-ui/svelte";
  import { generatePDF } from "$lib/utils";
  import Viewscale from "./viewscale.svelte";
  import { demoState, ui } from "$lib/state/index.svelte";
  import { authStore, authActions } from "$lib/state/auth.js";

  let theme = $state();
  let showUserMenu = $state(false);
  let showMobileMenu = $state(false);

  onMount(() => theme = localStorage.theme);

  const toggleTheme = () => {
    theme = theme == "dark" ? "light" : "dark";
    localStorage.theme = theme;
    const htmlElement = document.querySelector("html");
    if (htmlElement) {
      htmlElement.className = theme as string;
    }
  };

  const setActive = (x: string) => {
    document.body.style.overflow = x == "split" ? "hidden" : "visible";
    ui.mode = x;
  };

  const handleDemo = (x: any) => {
    demoState[x.target.checked ? "fill" : "empty"]();
  };

  const handleLogout = () => {
    authActions.logout();
    showUserMenu = false;
    showMobileMenu = false;
  };

  // Subscribe to auth store
  let isAuthenticated = $derived($authStore.isAuthenticated);
  let user = $derived($authStore.user);
</script>

<!-- Mobile Navbar -->
<div>
  <nav class="md:hidden p3 border-b border-border flex items-center justify-between sticky top-0 z-10 bg-bg">
    <a class="flex items-center gap-2" href="/">
      <i class="i-icon-park-solid:flashlamp bg-info text-xl"></i>
      <strong class="text-sm">ResuMate</strong>
    </a>

    <div class="flex items-center gap-2">
      <button
        class="btn-soft-eqlg rounded-full"
        aria-label="toggle dark mode"
        onclick={toggleTheme}
      >
        <div
          class={theme == "dark"
          ? "i-line-md:sun-rising-twotone-loop"
          : "i-line-md:moon-twotone-loop"}
        >
        </div>
      </button>

      {#if isAuthenticated}
        <button
          class="btn-soft-eqlg rounded-full"
          aria-label="mobile menu"
          onclick={() => showMobileMenu = !showMobileMenu}
        >
          <i class="i-material-symbols:menu"></i>
        </button>
      {:else}
        <a href="/login" class="btn-soft px-3 py-1 text-sm">Login</a>
      {/if}
    </div>
  </nav>

  {#if showMobileMenu && isAuthenticated}
    <div class="md:hidden bg-bg border-b border-border p-4 space-y-3 max-h-[calc(100vh-60px)] overflow-y-auto">
      <a href="/templates" class="block p-2 rounded hover:bg-secondary">Templates</a>
      
      {#if page.url.pathname == "/"}
        <div class="space-y-2">
          <Viewscale />
          
          <label for="demoswitch-mobile" class="brd flex items-center gap-2 p2 px3 rounded cursor-pointer">
            <input
              type="checkbox"
              class="checkbox-sm"
              id="demoswitch-mobile"
              onchange={handleDemo}
            />
            Demo
          </label>

          <Tabs value={ui.mode} setValue={setActive}>
            <TabsList class="p1 tab-(p2 px2 text-sm) tabon-(brd)">
              <Tab value="split"><i class="i-material-symbols:splitscreen-left"></i>
                Split</Tab>
              <Tab value="tab"> <i class="i-gravity-ui:layout-tabs"></i> Tabbed</Tab>
            </TabsList>
          </Tabs>

          <Btn
            iconL="i-tabler:download"
            txt="Download"
            class="btn-primary w-full"
            onclick={generatePDF}
          />
        </div>
      {/if}

      <div class="border-t border-border pt-2">
        <div class="px-4 py-2 text-sm">
          <div class="font-medium">{user?.name}</div>
          <div class="text-gray-500 text-xs">{user?.email}</div>
        </div>
        <button
          class="block w-full text-left px-4 py-2 text-sm hover:bg-secondary rounded"
          onclick={handleLogout}
        >
          Sign out
        </button>
      </div>
    </div>
  {/if}
</div>

<!-- Desktop Navbar -->
<nav class="hidden md:flex p3 border-b border-border items-center sticky top-0 z-10 bg-bg">
  <a class="frow" href="/">
    <i class="i-icon-park-solid:flashlamp bg-info text-xl"></i>
    <strong>ResuMate</strong>
  </a>

  <a href="/templates" class="mr-auto ml2 hidden lg:block">Templates</a>

  <!-- Authentication section -->
  {#if isAuthenticated}
    <div class="relative">
      <button
        class="btn-soft-eqlg rounded-full"
        aria-label="user menu"
        onclick={() => showUserMenu = !showUserMenu}
      >
        <i class="i-material-symbols:account-circle"></i>
      </button>
      
      {#if showUserMenu}
        <div class="absolute right-0 mt-2 w-48 bg-white rounded-md shadow-lg py-1 z-20 border">
          <div class="px-4 py-2 text-sm text-gray-700 border-b">
            <div class="font-medium">{user?.name}</div>
            <div class="text-gray-500">{user?.email}</div>
          </div>
          <button
            class="block w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
            onclick={handleLogout}
          >
            Sign out
          </button>
        </div>
      {/if}
    </div>
  {:else}
    <div class="frow gap-2">
      <a href="/login" class="btn-soft px-3 py-1 text-sm">Login</a>
      <a href="/signup" class="btn-primary px-3 py-1 text-sm">Sign Up</a>
    </div>
  {/if}

  {#if page.url.pathname == "/"}
    <Viewscale />

    <label for="demoswitch" class="brd frow p2 px3 rounded hidden lg:flex">
      <input
        type="checkbox"
        class="checkbox-sm"
        id="demoswitch"
        onchange={handleDemo}
      />
      Demo
    </label>

    <Tabs value={ui.mode} setValue={setActive}>
      <TabsList class="p1 tab-(p2 px2 text-sm) tabon-(brd)">
        <Tab value="split"><i class="i-material-symbols:splitscreen-left"></i>
          <span class="hidden lg:inline">Split</span></Tab>
        <Tab value="tab"> <i class="i-gravity-ui:layout-tabs"></i> <span class="hidden lg:inline">Tabbed</span></Tab>
      </TabsList>
    </Tabs>

    <Btn
      iconL="i-tabler:download"
      txt="Download"
      class="btn-primary hidden lg:flex"
      onclick={generatePDF}
    />
  {/if}

  <button
    class="btn-soft-eqlg rounded-full"
    aria-label="toggle dark mode"
    onclick={toggleTheme}
  >
    <div
      class={theme == "dark"
      ? "i-line-md:sun-rising-twotone-loop"
      : "i-line-md:moon-twotone-loop"}
    >
    </div>
  </button>
</nav>
