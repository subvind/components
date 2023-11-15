<script lang="ts">
  import { onMount } from 'svelte';

	export let organization: any;

  import { jwtDecode} from 'jwt-decode';

  let accessToken: any = undefined
  let decoded: any = undefined

  onMount(() => {
    accessToken = localStorage.getItem('access_token');
    if (accessToken) {
      decoded = jwtDecode(accessToken);
    }

		var elems = document.querySelectorAll('.collapsible');
		var instances = M.Collapsible.init(elems, {});
	})
</script>


<li><div class="divider"></div></li>
<li><a class="subheader">Auth</a></li>
{#if organization && decoded}
	{#if decoded.type === 'account'}
		<li><a href={`https://${organization.homeHostname}/accounts/${decoded.accountname}`} target="_self" class="waves-effect" ><i class="material-icons">account_circle</i>{decoded.accountname}</a></li>
	{:else}
		<li><a href={`https://${organization.homeHostname}/users/${decoded.username}`} target="_self" class="waves-effect" ><i class="material-icons">assignment_ind</i>{decoded.username}</a></li>
	{/if}
	<li><a href={`/auth/logout`} target="_self" class="waves-effect" ><i class="material-icons">lock_outline</i> Logout</a></li>
{:else}
<li><a href={`/auth/login`} target="_self" class="waves-effect" ><i class="material-icons">lock_open</i> Login</a></li>
<li><a href={`/auth/register`} target="_self" class="waves-effect" ><i class="material-icons">vpn_key</i> Register</a></li>
{/if}


<style>
	.collapsible-header {
		height: 3.2em;
		padding: 0 32px;
	}
</style>
