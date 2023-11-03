<script lang="ts">
  import { onMount } from 'svelte';

	let categories: any;

	onMount(async () => {
		let erpHostname = window.location.hostname
		if (erpHostname === 'localhost') {
			erpHostname = 'store.subvind.com'
		}
    const response = await fetch(`https://api.subvind.com/categories/erpHostname/${erpHostname}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (response.ok) {
      categories = await response.json();
    } else {
			const errorData = await response.json();
      alert(errorData.error);
    }

    var elems = document.querySelectorAll('.collapsible');
    var instances = M.Collapsible.init(elems, {});
	})
</script>

<li><div class="divider"></div></li>
<li><a class="subheader">Categories</a></li>
<li class="black-text">
  <ul class="collapsible">
    {#if categories}
      {#each categories.data as category}
        {#if !category.parentCategory}
          <li>
            <div class="collapsible-header">{category.name}</div>
            <div class="collapsible-body">
              {#if category.subCategories}
                {#each category.subCategories as subCategory}
                  <li><a class="waves-effect" href={`/categories/${subCategory.slug}`} target="_self"><i class="material-icons">subdirectory_arrow_right</i>{subCategory.name}</a></li>
                {/each}
              {/if}
            </div>
          </li>
        {/if}
      {/each}
    {/if}
  </ul>
</li>

<style>
	.collapsible-header {
		height: 3.2em;
		padding: 0 32px;
	}
</style>