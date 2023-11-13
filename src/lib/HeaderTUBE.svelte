<script lang="ts">
  import { onMount } from 'svelte';

	import { MenuPlaylists, Menu, Controls } from './index.js'

	export let organization: any;

  let channel: any = null;

	onMount(async () => {
    var elems = document.querySelectorAll('.sidenav');
    var instances = M.Sidenav.init(elems, {});

    await fetch(`/data/profile.json`)
      .then(response => response.json())
      .then(results => {
        console.log(`profile.json`, results)
        channel = results
      }).catch(error => {
        console.log(error);
        return [];
      });
	})
</script>

<header>
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
				{#if organization}
					<div class="describe">
						{@html organization.description}
					</div>
				{/if}
				<MenuPlaylists />
				<Menu organization={organization} />
			</ul>
			{#if organization}
				<a href="#" data-target="slide-out" class="brand-logo sidenav-trigger left"><i class="material-icons">menu</i>{organization.displayName}</a>
			{/if}
			<Controls organization={organization} />
		</div>
	</nav>
</header>

<div class="banner">
	{#if channel}
		<img src={channel.brandingSettings.image.bannerExternalUrl} alt="">
	{/if}
</div>
<div class="container">
	{#if channel}
		<div class="row">
			<div class="col s12">
				<a href="/"><img src={channel.snippet.thumbnails.medium.url} alt="" class="avatar"></a>
				<div class="hide-on-med-and-down">
					<a href={`https://youtube.com/${channel.snippet.customUrl}`} target="_blank"><button class="btn right red lighten-2">SUBSCRIBE</button></a>
					<a href="/channel-guide"><button class="btn white black-text right" style="margin-right: 0.5em">CHANNEL GUIDE</button></a>
				</div>
		
				<h4>{channel.snippet.title}</h4>
				<p>
					Views: <strong>{channel.statistics.viewCount}</strong> •
					Subscribers: <strong>{channel.statistics.subscriberCount}</strong> • 
					Videos: <strong>{channel.statistics.videoCount}</strong>
				</p>
				<p>
					{channel.brandingSettings.channel.description}
				</p>
			</div>
		</div>
		<div class="row hide-on-large-only">
			<div class="col s6">
				<a href={`https://youtube.com/${channel.snippet.customUrl}`} target="_blank"><button class="btn red lighten-2" style="width: 100%;">SUBSCRIBE</button></a>
			</div>
			<div class="col s6">
				<a href="/channel-guide"><button class="btn white black-text" style="width: 100%">CHANNEL GUIDE</button></a>
			</div>
		</div>
	{/if}
</div>

<style>
	header {
    position: relative;
  }

	nav .sidenav-trigger {
		display: initial !important;
	}
	
	.describe {
    margin: 0px 0.5em;
    color: rgb(17, 17, 17);
    line-height: 2em;
    text-align: center;
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

	.container {
		margin: 0 auto;
		background: #333;
		padding: 1em;
		padding-bottom: 0;
		color: #ccc;
		position: relative;
		border: 3px solid #333;
		border-bottom: 0px;
		overflow: hidden;
	}

	p {
		margin: 0.5em 0;
		color: #888;
	}

	.avatar {
		float: left;
		width: 150px;
		border: 3px solid #333;
		border-radius: 10em;
		margin-right: 1em;
	}

	.banner {
		width: 100%;
		height: 400px;
		min-width: 938px;
		overflow: hidden;
		display: flex;
		align-items: center;
		margin-bottom: -6em;
		border-bottom: 3px solid #333;
	}

	.banner img {
		width: 100%;
	}
</style>
