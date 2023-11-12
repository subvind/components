<script lang="ts">
  import { onMount } from 'svelte';

  export let load: string = 'homenomy';
  export let organization;

  onMount(() => {
    var elems = document.querySelectorAll('.dropdown-trigger0528');
    var instances = M.Dropdown.init(elems, {
      hover: true,
      constrainWidth: false
    });
  })
</script>

<a href="#" class="brand-logo center dropdown-trigger0528" data-target='dropdown0528'>
  {#if load === 'homenomy'}
    <span class="yellow">nomy</span>.<span class="red">HOME</span>
  {/if}
  {#if load === 'erpnomy'}
    <span class="yellow">nomy</span>.<span class="green">E</span><span class="red">R</span><span class="blue">P</span>
  {/if}
  {#if load === 'tubenomy'}
    <span class="yellow">nomy</span>.<span class="red">TUBE</span>
  {/if}
  {#if load === 'desknomy'}
    <span class="yellow">nomy</span>.<span class="red">DESK</span>
  {/if}
</a>

<!-- Dropdown Structure -->
<ul id='dropdown0528' class='dropdown-content'>
  {#if organization}
    <li><a href={`https://homenomy.${organization.backendHostname}`}>nomy.HOME</a></li>
    <li><a href={`https://erpnomy.${organization.backendHostname}`}>nomy.ERP</a></li>
    <li><a href={`https://tubenomy.${organization.backendHostname}`}>nomy.TUBE</a></li>
    <li><a href={`https://desknomy.${organization.backendHostname}`}>nomy.DESK</a></li>
  {/if}
</ul>

<style>
  .yellow {
    color: yellow;
    background-color: transparent !important;
  }
  .green {
    color: green;
    background-color: transparent !important;
  }
  .blue {
    color: #039be5;
    background-color: transparent !important;
  }
  .red {
    color: red;
    background-color: transparent !important;
  }
  .purple {
    color: purple;
    background-color: transparent !important;
  }
</style>