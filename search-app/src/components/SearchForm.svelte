<script>
  import { selects } from './selection.js';
  import { isSearching, SearchTerm, fields } from './store';

  function handleOnSubmit() {
    $isSearching = true;
    $fields = $fields;
  }
  function dropdown() {}

  import Modal, { bind } from 'svelte-simple-modal';
  import { writable } from 'svelte/store';
  import Filter from './modal/Filter.svelte';
  const modal = writable(null);
  const showModal = () => modal.set(bind(Filter));
</script>

<div class="wrapper-spacer" />
<div class="wrapper-bar">
  <Modal show={$modal}>
    <button class="menubar" on:click={showModal} aria-label="Start search"
      ><svg
        xmlns="http://www.w3.org/2000/svg"
        height="48"
        width="48"
        fill="#fff"
        ><path d="M6 36V33H42V36ZM6 25.5V22.5H42V25.5ZM6 15V12H42V15Z" /></svg
      ></button
    >
  </Modal>
  <form class="form" on:submit|preventDefault={handleOnSubmit}>
    <div class="wrapper svelte-iqmikt">
      <input
        class="searchBox svelte-iqmikt"
        type="search"
        name="search"
        spellcheck="true"
        placeholder="           Search"
        aria-label="Search case studies"
        bind:value={$SearchTerm}
        required
      />

      <button
        class="button svelte-iqmikt"
        disabled={$SearchTerm === ''}
        type="submit"
        aria-label="Start search"
        title="Click to search"
        ><svg
          class="icon"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="black"
          width="24px"
          height="24px"
          ><path d="M0 0h24v24H0z" fill="none" /><path
            d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"
          /></svg
        ></button
      >
    </div>
    <!-- dropdown -->

    <!-- <div class="dropdown">
      <ul class="checbox-filters">
        {#each selects as { n, id, label } (id)}
          <li class="check-svelte">
            <input
              class="checkbox-svelte"
              type="checkbox"
              bind:group={$fields}
              value={n}
            />
            <label class="checkbox-label" for={id}> {label} </label>
          </li>
        {/each}
      </ul>
    </div> -->
    <!-- dropdown -->
  </form>
</div>

<style>
  .wrapper-bar {
    display: grid;
    grid-template-columns: repeat(2, 100px);
    padding: 0;
  }
  .menubar {
    background: none;
    border: 0;

    cursor: pointer;
  }
  /* .menubar {
    position: absolute;

    left: 0;
    top: 0;
    height: 2.875rem;
    width: 2.875rem;
    padding: 0;
    background: none;
    border: 0 none;
    border-radius: 0 0.375rem 0.375rem 0;
    padding: 0.6875rem;
    cursor: pointer;
  } */
  .menubar > svg > rect {
    fill: white;
  }
  .checbox-filters {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    padding: 0;
  }

  .check-svelte {
    padding-left: 20px;

    font-size: 16px;
  }
  form ul li {
    display: flex;
    align-items: center;
  }

  .checkbox-svelte {
    -webkit-appearance: none;
    background-color: #fafafa;
    border: 1px solid #cacece;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05),
      inset 0px -15px 10px -12px rgba(0, 0, 0, 0.05);
    padding: 8px;
    border-radius: 3px;
    display: inline-block;
    position: relative;
  }
  .checkbox-svelte:active,
  .checkbox-svelte:checked:active {
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05),
      inset 0px 1px 3px rgba(0, 0, 0, 0.1);
  }

  .checkbox-svelte:checked {
    background-color: #e9ecee;
    border: 1px solid #adb8c0;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05),
      inset 0px -15px 10px -12px rgba(0, 0, 0, 0.05),
      inset 15px 10px -12px rgba(255, 255, 255, 0.1);
    color: #99a1a7;
  }
  .checkbox-svelte:checked:after {
    content: '\2714';

    font-size: 18px;
    position: absolute;
    top: -4px;
    left: 1px;

    color: #4e4e4e;
  }
  .checkbox-svelte:hover {
    transform: scale(1.2, 1.2);
  }
  .checkbox-label {
    font-family: 'Work Sans', work-sans, sans-serif;
    font-size: 1.15rem;
    line-height: 1.2rem;
    padding: 8px;
    color: #1f1f1f;
  }

  .form {
    min-width: 450px;
    width: 100%;
    margin: 0 auto;
    padding: 10px;
  }
  .wrapper.svelte-iqmikt {
    position: relative;
    border-radius: 0.375rem;
    background: #fff;
  }
  .searchBox.svelte-iqmikt {
    display: inline-block;
    width: 100%;
    padding: 0.75rem 2.875rem 0.75rem 0.75rem;
    margin: 0;
    font-family: 'Lato', sans-serif;
    font-size: 1.125rem;
    color: #5f7380;
    border: 1px solid #c4cbcf;
    border-radius: 0.375rem;
    box-shadow: 0px 8px 9px -6px rgb(95 115 128 / 44%);
  }
  .button.svelte-iqmikt {
    position: absolute;
    right: 0;
    top: 0;
    height: 2.875rem;
    width: 2.875rem;
    padding: 0;
    background: none;
    border: 0 none;
    border-radius: 0 0.375rem 0.375rem 0;
    padding: 0.6875rem;
    cursor: pointer;
  }
  .button.svelte-iqmikt:disabled {
    cursor: not-allowed;
  }

  .button.svelte-iqmikt:disabled > svg {
    fill: #c4cbcf;
  }
</style>
