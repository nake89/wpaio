<script lang="ts">
  import Fa from 'svelte-fa'
  import { faGithub, faTwitter } from '@fortawesome/free-brands-svg-icons'
  import { faHome } from '@fortawesome/free-solid-svg-icons'

  import { Input, Switch, Progress } from 'spaper';
	export let pageNum = localStorage.getItem("pageNum");
	export let maxPageNum = localStorage.getItem("maxPageNum");
  function changePageNum() {
    localStorage.setItem("pageNum",pageNum);
  } 
  function changeMaxPageNum() {
    localStorage.setItem("maxPageNum",maxPageNum);
  } 
  function saveShowProgress() {
    localStorage.setItem("showProgress",String(showProgress));
  }
  let percentage = "0";
  function adjustPercentage() {
    if (pageNum && maxPageNum) {
      percentage = ((Number(pageNum) / Number(maxPageNum))*100).toFixed(2);
    }
  }
  let showAdvancedOptions = false;
  let showProgress = localStorage.getItem("showProgress") ? (localStorage.getItem("showProgress") === "true") : false;
  $: {showProgress; saveShowProgress();}
  $: {pageNum; adjustPercentage();}
  $: {maxPageNum; adjustPercentage();}
</script>

<main>
	<h1>What Page Am I On?</h1>
  <div class="form-group">
    <label for="pageNum">Current page #:</label><br>
    <Input placeholder="Page number" id="pageNum" type="number" bind:value={pageNum} on:input={changePageNum} block class="margin" />
    {#if showProgress}
      <Progress striped type="secondary" showValue value={Math.floor(Number(percentage))} class="margin" />
    {/if}
    <div class="margin">
      <Switch inline round bind:checked={showAdvancedOptions}>Advanced Options</Switch>
    </div>
    {#if showAdvancedOptions}
    <br>
    <div class="margin">
      <label for="maxPageNum">How many pages does your book have?:</label><br>
      <Input placeholder="Page number" id="maxPageNum" type="number" bind:value={maxPageNum} on:input={changeMaxPageNum} block />
      <div class="margin">
        <Switch inline round bind:checked={showProgress}>Show Progress:</Switch>
      </div>
    </div>
    {/if}
  </div>
  <br><br>
  <div class="topMargin">
    <button onclick="location.href='https://kevinkivi.com'"><Fa icon={faHome} /></button>
    <button onclick="location.href='https://github.com/nake89/wpaio'"><Fa icon={faGithub} /></button>
    <button onclick="location.href='https://twitter.com/nake89'"><Fa icon={faTwitter} /></button>
  </div>
</main>

<style>
  .topMargin {
    margin-top: 20px;
  }
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		font-size: 4em;
		font-weight: 100;
	}

</style>
