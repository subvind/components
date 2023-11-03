<script lang="ts">
  import { onMount } from 'svelte';

	export let organization: any;

	onMount(async () => {
		var elems = document.querySelectorAll('.dropdown-trigger');
		var instances = M.Dropdown.init(elems, {
			constrainWidth: false,
		});
	})
</script>

<ul id="nav-mobile" class="right">
	<!-- Dropdown Trigger -->
	<li>
		<div class="logo">
			{#if organization}
				{#if organization.orgPhoto}
					<img src={`https://s3.us-east-2.amazonaws.com/${organization.orgname}.${organization.orgPhoto.bucket.name}/${organization.orgPhoto.filename}`} alt="logo" class="dropdown-trigger" data-target='dropdown1'>
				{:else}
					<img src="/anchor.png" alt="logo" class="dropdown-trigger" data-target='dropdown1'>
				{/if}
			{/if}
		</div>
	</li>

	<!-- Dropdown Structure -->
	<ul id='dropdown1' class='dropdown-content'>
		{#if organization}
			{#if organization.ebayUser}
				<li><a href={`https://www.ebay.com/usr/${organization.ebayUser}`} target="_blank">ebay.com/usr/{organization.ebayUser}</a></li>
			{/if}
			{#if organization.etsyShop}
				<li><a href={`https://www.etsy.com/shop/${organization.etsyShop}`} target="_blank">etsy.com/shop/{organization.etsyShop}</a></li>
			{/if}
			{#if organization.youtubeChannel}
				<li><a href={`https://www.youtube.com/${organization.youtubeChannel}`} target="_blank">youtube.com/{organization.youtubeChannel}</a></li>
			{/if}
		{/if}
	</ul>
</ul>

<style>
	.logo {
		max-height: 3.2em;
		width: 3.2em;
		margin: 0.5em 0.5em 0;
		border-radius: 10em;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
	}

	.logo img {
    width: auto;
    max-width: 100%;
    object-fit: contain;
	}
</style>
