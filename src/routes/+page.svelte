<script lang="ts">
  import { onMount } from "svelte";

  import { AuthRegister } from "$lib/index.js"
  import { AuthLogin } from "$lib/index.js"
  import { AuthAccountLogin } from "$lib/index.js"

	let organization: any;

  onMount(async () => {
    let deskHostname = window.location.hostname
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

<!-- <NavModules load="erpnomy" organization={organization} /> -->

<!-- <AuthRegister organization={organization} /> -->
<!-- <AuthLogin organization={organization} /> -->
<!-- <AuthAccountLogin organization={organization} /> -->

<div class="container">
  <h1>Welcome to your library project</h1>
  <p>Create your package using @sveltejs/package and preview/showcase your work with SvelteKit</p>
  <p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
</div>
