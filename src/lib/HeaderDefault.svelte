<script lang="ts">
  import { onMount } from 'svelte';

	import { Auth, Menu, Controls } from './index.js'

	export let organization: any;

	onMount(async () => {
    var elems = document.querySelectorAll('.sidenav');
    var instances = M.Sidenav.init(elems, {});
	})
</script>

<header class="navbar-fixed">
	<nav class="grey darken-3">
		<div class="nav-wrapper">
			<ul id="slide-out" class="sidenav">
				<nav class="grey darken-3" style="max-height: 64px;">
					<div class="nav-wrapper">
						{#if organization}
							<a href="/" target="_self" class="brand-logo" style="width: 100%; text-align: center;">{organization.shortName || 'PORTAL'}</a>
						{/if}
					</div>
				</nav>
				<br />
				{#if organization}
					<div class="describe">
						{@html organization.description}
					</div>
				{/if}
				<Auth organization={organization} />
				<Menu organization={organization} />
			</ul>
			{#if organization}
				<a href="#" data-target="slide-out" class="brand-logo sidenav-trigger left"><i class="material-icons">menu</i>{organization.displayName}</a>
			{/if}
			<Controls organization={organization} />
		</div>
	</nav>
</header>


<style>
	header {
    position: relative;
  }

	nav .sidenav-trigger {
		display: initial !important;
	}
	
	.describe {
    margin: 0.5em;
    color: rgb(17, 17, 17);
    line-height: 1.5em;
    text-align: center;
	}

	:global(.sidenav-overlay) {
		z-index: 1;
	}
</style>
