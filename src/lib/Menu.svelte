<script lang="ts">
  import { onMount } from 'svelte';

	export let organization: any;

	onMount(async () => {
		var elems = document.querySelectorAll('.collapsible');
		var instances = M.Collapsible.init(elems, {});
	})
</script>


<li><div class="divider"></div></li>
<li><a class="subheader">Menu</a></li>
{#if organization.menu}
	{#each organization.menu as menu}
		<li><a href={menu.url} target="_self" class="waves-effect" ><i class="material-icons">{menu.icon}</i>{menu.name}</a></li>
	{/each}
{:else}
	{#if organization.homepageLink}
		<li><a href={organization.homepageLink || '/'} target="_self" class="waves-effect" ><i class="material-icons">home</i>Homepage</a></li>
	{/if}
	{#if organization.isErpModule}
		{#if organization.erpHostname}
			<li><a href={`https://${organization.erpHostname}`} target="_self" class="waves-effect"><i class="material-icons">local_grocery_store</i>Store</a></li>
		{:else}
			<li><a href={`https://${organization.orgname}.erpnomy.com`} target="_self" class="waves-effect"><i class="material-icons">local_grocery_store</i>Store</a></li>
		{/if}
	{/if}
	{#if organization.isTubeModule}
		{#if organization.tubeHostname}
			<li><a href={`https://${organization.tubeHostname}`} target="_self" class="waves-effect"><i class="material-icons">videocam</i>Videos</a></li>
		{:else}
			<li><a href={`https://${organization.orgname}.tubenomy.com`} target="_self" class="waves-effect"><i class="material-icons">videocam</i>Videos</a></li>
		{/if}
	{/if}
	{#if organization.isDeskModule}
		{#if organization.deskHostname}
			<li><a href={`https://${organization.deskHostname}`} target="_self" class="waves-effect"><i class="material-icons">verified_user</i>Client Area</a></li>
		{:else}
			<li><a href={`https://${organization.orgname}.desknomy.com`} target="_self" class="waves-effect"><i class="material-icons">verified_user</i>Client Area</a></li>
		{/if}
	{/if}
	{#if organization.contactCenterEmail}
		<li><a href="/contact-center" target="_self" class="waves-effect"><i class="material-icons">local_phone</i>Contact Center</a></li>
	{/if}
{/if}

<li><div class="divider"></div></li>
<li><a class="subheader">Extra</a></li>
<li><a class="waves-effect" href="/privacy-policy" target="_self">Privacy Policy</a></li>
<li><a class="waves-effect" href="/terms-and-conditions" target="_self">Terms & Conditions</a></li>
<li class="black-text">
	<ul class="collapsible">
		<li>
			<div class="collapsible-header" style="padding: 0 2em;">Control Panels</div>
			<div class="collapsible-body">
				{#if organization.isHomeModule}
					<li><a class="waves-effect" href={`https://homenomy.subvind.com`} target="_self"><i class="material-icons">subdirectory_arrow_right</i>nomy.HOME</a></li>
				{/if}
				{#if organization.isErpModule}
					<li><a class="waves-effect" href={`https://erpnomy.subvind.com`} target="_self"><i class="material-icons">subdirectory_arrow_right</i>nomy.ERP</a></li>
				{/if}
				{#if organization.isTubeModule}
					<li><a class="waves-effect" href={`https://tubenomy.subvind.com`} target="_self"><i class="material-icons">subdirectory_arrow_right</i>nomy.TUBE</a></li>
				{/if}
				{#if organization.isDeskModule}
					<li><a class="waves-effect" href={`https://desknomy.subvind.com`} target="_self"><i class="material-icons">subdirectory_arrow_right</i>nomy.DESK</a></li>
				{/if}
			</div>
		</li>
	</ul>
</li>


<style>
	.collapsible-header {
		height: 3.2em;
		padding: 0 32px;
	}
</style>
