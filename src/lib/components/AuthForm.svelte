<script lang="ts">
	import { Button } from '$components';
	import type { ActionData } from '../../routes/register/$types';

	interface AuthFormProps {
		isRegistration: boolean;
		form: ActionData;
	}
	let { isRegistration, form }: AuthFormProps = $props();
</script>

<div class="default-margin auth-container">
	<h1 class="mb-l">{isRegistration ? 'Register' : 'Login'}</h1>
	<div class="form-and-social-login">
		<form class="auth-form" method="POST">
			{#if form && form.errors?.length}
				{#each form.errors as error}
					<div class="auth-error"><p>{error}</p></div>
				{/each}
			{/if}
			{#if isRegistration}
				<input type="text" placeholder="Name" name="name" />
			{/if}
			<input type="text" placeholder="Email" name="email" />
			<input type="password" placeholder="Password" name="password" />
			{#if isRegistration}
				<input type="password" placeholder="Confirm password" name="passwordConfirmation" />
			{/if}
			<Button type="submit">{isRegistration ? 'Register' : 'Login'}</Button>
			{#if isRegistration}
				<p class="auth-hint mt-s">Already have an account? <a href="/login">Log In.</a></p>
			{:else}
				<p class="auth-hint mt-s">Do not have an account yet? <a href="/login">Register.</a></p>
			{/if}
		</form>
		<form class="social-login"></form>
	</div>
</div>

<style>
	.auth-container {
		margin-top: 80px;
	}
	.form-and-social-login {
		display: flex;
	}
	.auth-form {
		display: flex;
		flex-direction: column;
		align-items: start;
		border-right: 1px solid grey;
		padding-right: 80px;
		width: 40%;
	}
	.auth-form input {
		width: 100%;
		margin-bottom: 12px;
	}

	.auth-form input:last-of-type {
		margin-bottom: 30px;
	}
	.auth-hint {
		font-size: 16px;
		color: grey;
	}
	.auth-error {
		background-color: rgba(122, 35, 35);
		color: white;
		font-size: 18px;
		border-radius: 12px;
		padding: 12px;
		width: 100%;
		margin-bottom: 8px;
	}
	.auth-error:last-of-type {
		margin-bottom: 16px;
	}
	.social-login {
		padding-left: 80px;
		width: 40%;
	}
</style>
