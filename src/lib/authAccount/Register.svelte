<script lang="ts">
  import { onMount } from 'svelte';
  import { jwtDecode } from 'jwt-decode';

  let loading: boolean = false;
  let accountname = ''
  let firstName = ''
  let lastName = ''
	let email = ''
  let password = ''
  let passwordRepeat = ''
  export let organization: any;

	async function register(event: any) {
    event.preventDefault()

    if (accountname === '') return alert('Accountname must be defined.')
    if (firstName === '') return alert('First name must be defined.')
    if (lastName === '') return alert('Last name must be defined.')
    if (email === '') return alert('Email must be defined.')
    if (password === '') return alert('Password must be defined.')
    if (passwordRepeat === '') return alert('Confirm Password must be defined.')
    if (passwordRepeat !== password) return alert('Passwords must match.')
    
    loading = true

    try {
      const response = await fetch('https://api.subvind.com/accounts', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          accountname,
          firstName,
          lastName,
          email,
          password,
          organization: {
            id: organization.id
          }
        }),
      });

      if (response.ok) {
        const response = await fetch('https://api.subvind.com/auth/accountLogin', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            email,
            password,
            organizationId: organization.id
          }),
        });

        if (response.ok) {
          let res = await response.json();

          console.log('access_token', res.access_token)

          // Save the access token to localStorage
          localStorage.setItem('access_token', res.access_token);

          // Decode the JWT
          let decodedToken: any = jwtDecode(res.access_token);

          console.log('decoded_token', decodedToken)

          // You can redirect the user to a new page or handle the success scenario in your app
          window.location.href = `/auth/success`
        } else {
          const errorData = await response.json();
          alert(errorData.error);
        }
      } else {
        const errorData = await response.json();
        alert(errorData.error);
      }
    } catch (error) {
      console.error('Error registering user:', error);
      alert('An error occurred during submission.');
    }

    loading = false
  }

  onMount(async () => {

  })
</script>

<div class="contain">
  <div class="header">
    <h1 class="title">
      Register
    </h1>
    {#if organization}
      {organization.frontendHostname}
    {:else}
      authentication
    {/if}
  </div>
  <form class="card" on:submit={(e) => register(e)}>
    <div class="card-content">
      <div class="row">
        <div class="input-field col s12">
          <input id="accountname" type="text" class="validate" bind:value={accountname}>
          <label for="accountname">Username</label>
        </div>
        <div class="input-field col s6">
          <input id="firstName" type="text" class="validate" bind:value={firstName}>
          <label for="firstName">First Name</label>
        </div>
        <div class="input-field col s6">
          <input id="lastName" type="text" class="validate" bind:value={lastName}>
          <label for="lastName">Last Name</label>
        </div>
        <div class="input-field col s12">
          <input id="email" type="email" class="validate" bind:value={email}>
          <label for="email">Email</label>
        </div>
        <div class="input-field col s12">
          <input id="password" type="password" class="validate" bind:value={password}>
          <label for="password">Password</label>
        </div>
        <div class="input-field col s12">
          <input id="passwordRepeat" type="password" class="validate" bind:value={passwordRepeat}>
          <label for="passwordRepeat">Password Confirm</label>
        </div>
        <br />
        {#if loading}
          <button style="margin-left: 1em;" class="waves-effect btn disabled">Loading</button>
        {:else}
          <button style="margin-left: 1em;" type='submit' class="waves-effect yellow black-text lighten-2 btn">Submit</button>
        {/if}
      </div>
    </div>
  </form>
  <div>
    <a href="/auth/login" class="waves-effect black white-text btn" style="float: right;">Login</a>
    <br />
    <br />
    <a href="/password-recovery" class="waves-effect white black-text btn" style="float: right;">Password Recovery</a>
    <br />
    <br />
    <br />
    <br />
  </div>
</div>

<style>
  .contain {
    max-width: 400px;
    margin: 0 auto;
  }

  .header {
    text-align: center;
  }

	.title {
		font-weight: 900;
		font-size: 2em;
		margin: 0;
	}

  .anchor {
    height: 150px;
   -webkit-filter: invert(1);
   filter: invert(1);
   text-align: center;
  }
</style>