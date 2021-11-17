<script>
  import { store } from './auth.ts'
  import Auth from '@aws-amplify/auth';
  let username = ""
  let password = ""
  let email = ""
  let promise
  function handleSubmit() {
    Auth.signUp({
      username,
      password,
      attributes: {
        email,
      },
    }).then(user => {
      $store = user //  save user object, representing a successful login
    })
  }
</script>
<div>
  <h1>Sign In</h1>
  <pre>{JSON.stringify($store, null, 2)}</pre>
  <form on:submit|preventDefault={handleSubmit}>
    <label>
      Username:
      <input type="text" bind:value={username} placeholder="your username"/>
    </label>
    <label>
      Password:
      <input type="password" bind:value={password} />
    </label>
    <label>
      Email:
      <input type="email" bind:value={email} />
    </label>
    <button type="submit">Submit</button>
  </form>
</div>
