<script lang="ts">
  import { onMount } from "svelte";

  import { HeaderDefault } from "$lib/index.js"
  import { FooterCommand } from "$lib/index.js"

	let organization: any;
	let deskHostname: any = '';

  onMount(async () => {
    deskHostname = window.location.hostname
    if (deskHostname === 'localhost') {
      deskHostname = 'client-area.subvind.com'
    }
    const response = await fetch(`https://api.subvind.com/organizations/deskHostname/${deskHostname}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (response.ok) {
      organization = await response.json();
    } else {
      const errorData = await response.json();
      alert(errorData.error);
    }
  })
</script>

{#if organization}
  <HeaderDefault organization={organization} />
{:else}
  <nav class="grey darken-3">
    <div class="nav-wrapper">
    </div>
  </nav>
{/if}

<slot />

<FooterCommand active="ERP" />

<style>
  :global(body) {
    background: #eee;
  }
</style>