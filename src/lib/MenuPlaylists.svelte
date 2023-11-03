<script lang="ts">
  import { onMount } from 'svelte';

	let playlists: any;

	onMount(async () => {
		let tubeHostname = window.location.hostname
		if (tubeHostname === 'localhost') {
			tubeHostname = 'videos.subvind.com'
		}
    const response = await fetch(`https://api.subvind.com/playlists/tubeHostname/${tubeHostname}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (response.ok) {
      playlists = await response.json();
    } else {
			const errorData = await response.json();
      alert(errorData.error);
    }

    var elems = document.querySelectorAll('.collapsible');
    var instances = M.Collapsible.init(elems, {});
	})
</script>

<li><div class="divider"></div></li>
<li><a class="subheader">Playlists</a></li>
<li class="black-text">
  <ul class="collapsible">
    {#if playlists}
      {#each playlists.data as playlist}
        {#if !playlist.parentPlaylist}
          <li>
            <div class="collapsible-header">{playlist.name}</div>
            <div class="collapsible-body">
              {#if playlist.subPlaylists}
                {#each playlist.subPlaylists as subPlaylist}
                  <li><a class="waves-effect" href={`/playlists/${subPlaylist.slug}`} target="_self"><i class="material-icons">subdirectory_arrow_right</i>{subPlaylist.name}</a></li>
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