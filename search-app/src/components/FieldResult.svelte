<script>
  import Selection from './Selection.svelte';
  import SearchFormClose from './SearchFormClose.svelte';
  import { Query } from '@sveltestack/svelte-query';
  import { SearchTerm, selection, fields, cols, pages } from './store';
  import { col } from './SelectColumn';
  import { LightPaginationNav } from './pagination/index.js';
  import NoResult from './NoResult.svelte';
  import { writable } from 'svelte/store';
  import Modal, { bind } from 'svelte-simple-modal';
  import Popup from './modal/Popup.svelte';
  import TableLoading from './TableLoading.svelte';
  import Skeleton from 'svelte-skeleton/Skeleton.svelte';

  const modal = writable(null);
  const showModal = () => modal.set(bind(Popup));

  let page = 1;
  let s;

  $: s = $SearchTerm.toLowerCase();
  $: page = $pages;
  $: field = $fields;

  const url = `https://www.callboxinc.com/wp-json/cbtk/v1/case-studies`;
  async function fetchPosts({ page = 1, s, field, $selection }) {
    if ($selection > 0) {
      const res = await fetch(
        `${url}?s=${s}&page=${page}&per_page=10&fields=${$selection}`
      );

      const data = await res.json();

      return data;
    } else {
      const res = await fetch(
        `${url}?s=${s}&page=${page}&per_page=10&fields=${field.join(',')}`
      );

      const data = await res.json();
      console.log(data);
      return data;
    }
  }

  $: queryOptions = {
    queryKey: ['seeMore', page, s, field, $selection],
    queryFn: () => fetchPosts({ page, s, field, $selection }),
    enabled: $SearchTerm !== '',
    keepPreviousData: true,
    cacheTime: 1000 * 60 * 5,
    refetchOnWindowFocus: false,
  };

  import { onMount } from 'svelte';
  let box;

  let yTop = 0;

  function parseScroll() {
    yTop = box.scrollTop;
    yHeight = box.clientHeight;
    yScroll = box.scrollHeight;
  }

  onMount(async () => parseScroll());

  import Table from './Table.svelte';
  import SearchForm from './SearchForm.svelte';
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@300;400;500;700&display=swap"
    rel="stylesheet"
  />
</svelte:head>

<!-- backup fect function-->
<!-- const res = await fetch(
  `${url}?s=${s}&page=${page}&per_page=10&fields=${field.join(',')}`
);

const data = await res.json();

return data; -->

<!-- <SearchFormClose /> -->

<div class="modal-wrapper">
  <div class="modal">
    <Selection />
  </div>
  <div class="dropdwn-selection">
    <Modal show={$modal}>
      <button class="modal-button" on:click={showModal}>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="#014e89"
          height="30"
          width="35"
          viewBox="-5 7 55 35"
          ><path
            d="M9 39H11.2L35.45 14.75L34.35 13.65L33.25 12.55L9 36.8ZM6 42V35.6L35.4 6.2Q36.25 5.35 37.525 5.375Q38.8 5.4 39.65 6.25L41.8 8.4Q42.65 9.25 42.65 10.5Q42.65 11.75 41.8 12.6L12.4 42ZM39.5 10.45 37.45 8.4ZM35.45 14.75 34.35 13.65 33.25 12.55 35.45 14.75Z"
          /></svg
        >
        <span class="modal-text">Edit Columns</span>
      </button>
    </Modal>
  </div>
</div>

<Query options={queryOptions}>
  <div slot="query" let:queryResult={{ data, isFetching, isError }}>
    <div class="cntnr">
      <div class="results svelte-fhxlyi">
        {#if isFetching}
          <h3><Skeleton height="35" width="350" /></h3>
          <div class="loading">
            <div
              class="table-wrapper"
              class:tableScrolled={yTop > 50}
              bind:this={box}
              on:scroll={parseScroll}
              on:mousemove={parseScroll}
            >
              <TableLoading />
            </div>
          </div>
        {:else if isError}
          <span>Error</span>
        {:else if data?.length}
          <h2 class="table-label">{data[0].label}</h2>

          <div class="table-container">
            <div
              class="table-wrapper"
              class:tableScrolled={yTop > 50}
              bind:this={box}
              on:scroll={parseScroll}
              on:mousemove={parseScroll}
            >
              <!-- this is table -->
              <Table
                tableData={data}
                tableheaderData={col}
                tableheader={$cols}
              />
              <!-- table helloworld -->
            </div>
          </div>
          {#if $selection > 0}
            <div class="area-2">
              <LightPaginationNav
                totalItems={data[0].total}
                pageSize={10}
                currentPage={$pages}
                limit={1}
                on:setPage={(e) => ($pages = e.detail.page)}
              />
            </div>
          {/if}
        {:else}
          <NoResult />
        {/if}
      </div>
    </div>
  </div>
</Query>

<!-- {#each data as { posts, id } (id)}
<table>
  <thead>
    <tr>
      <th>Title </th>
  
      {#each col as { id, label } (id)}
        {#each $cols as colsID}
          {#if colsID == id}
            <th>{label} </th>
          {/if}
        {/each}
      {/each}
    </tr>
  </thead>
  <tbody>
    {#each posts as post (post.id)}
      <tr>
        <td
          >{post.title}
          <button class="hide" on:click={() => onClick(post.id)}>
            show
          </button></td
        >
        {#each $cols as colsID}
          {#if colsID == 'client-location'}
            <td>{post.clientLocation}</td>
          {:else if colsID == 'product'}
            <td>{post.product}</td>
          {:else if colsID == 'campaign'}
            <td>
              {#each post.campaign as { label }}<span
                  >{label}</span
                >
              {/each}
            </td>
          {:else if colsID == 'link'}
            <td>{post.link}</td>
          {:else if colsID == 'linkUnlocked'}
            <td>{post.linkUnlocked}</td>
          {:else if colsID == 'pdf'}
            <td>{post.pdf}</td>
          {:else if colsID == 'clientHQ'}
            <td>{post.clientHQ}</td>
          {:else if colsID == 'target-location'}
            <td>{post.targetLocation}</td>
          {:else if colsID == 'target-industry'}
            <td>{post.targetIndustry}</td>
          {:else if colsID == 'target-dm'}
            <td>{post.targetDM}</td>
          {:else if colsID == 'results'}
            <td>
              {#each post.results as { label }}
                <span>{label}</span>
              {/each}</td
            >
          {/if}
        {/each}
      </tr>
    {/each}
  </tbody>
</table>
{/each} -->
<style>
  h3 {
    font-family: 'Work Sans', sans-serif;
    font-size: 2.25rem;
    font-weight: 700;
    color: #231f20;
    line-height: 2.75rem;
    text-align: center;
  }
  .cntnr {
    position: relative;
  }
  .table-label {
    position: absolute;
    top: -5.6rem;
    left: 2.5rem;
    font-family: 'open Sans', sans-serif;
    font-weight: 650;
    font-size: 2rem;
  }
  .modal {
    padding: 10px;
    padding-left: 53rem;
    padding-top: 50px;
  }
  .loading {
    padding-top: 55px;
  }
  .modal-button {
    display: grid;
    grid-template-columns: 0.4fr 1fr;
    padding-top: 20px;
    align-items: center;
  }
  .modal-text {
    color: #014e89;
    font-family: 'open Sans', sans-serif;
    font-weight: 650;
    font-size: 1rem;
    text-transform: capitalize;
  }

  .hide {
    display: none;
    position: absolute;
    bottom: 20px;
    background-color: #ffca09;
    border: 1px solid #ffca09;
    border-radius: 0.25rem;
    color: #004b84;
    text-transform: capitalize;
    padding: 0.175rem 0.5rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
  }
  .hide:hover {
    background-color: transparent;
  }

  tr:hover .hide {
    display: block;
  }
  table,
  td {
    border: 1px solid rgb(199, 198, 198);
    border-collapse: collapse;
    margin-bottom: 10px;
    padding: 10px;
    width: 100%;
    position: relative;
  }
  th {
    background-color: #014e89;
    color: white;
    border: 1px solid rgb(199, 198, 198);
    border-collapse: collapse;
    margin-bottom: 10px;
    padding: 10px;
    font-family: 'Lato', sans-serif;
    font-size: 1.15rem;
    line-height: 1.2rem;
  }
  tr:hover {
    background-color: #f1efef;
  }
  td {
    font-family: 'Work Sans', sans-serif;
    letter-spacing: initial;
  }

  .area-4 {
    color: #1d1d1d;
    padding-left: 0;
    display: flex;
    justify-content: flex-end;
    padding: 10px 0;
  }

  .table-container {
    overflow: auto;
    max-width: 75rem;
    width: 100%;
    padding-left: 2.5rem;
  }

  .table-wrapper {
    overflow: scroll;
    max-width: 1280px;
    max-height: 75vh;
    margin: 0 auto;
  }
  /* .table-wrapper::-webkit-scrollbar {
    display: none;
  } */

  th {
    color: #fff;
    background-color: #fff;
    font-weight: 600 !important;
    text-transform: uppercase;
    font-size: 1rem;
    line-height: 1.25rem;
    font-family: 'Work Sans', sans-serif;
    letter-spacing: 0.1px;
    padding: 15px 25px;
    min-width: 200px;
    text-align: center;
  }
  .tableScrolled table thead {
    position: sticky;
    top: -1px;
    left: 0;
    z-index: 999;
  }

  table thead th {
    background-color: #014e89;
  }
  table tbody tr td {
    font-size: 0.875rem;
  }
  tbody tr td:first-child {
    padding-bottom: 30px;
    height: 100px;
  }
  button.modal-button {
    background-color: #ffca09;
    border: 1px solid #ffca09;
    border-radius: 0.25rem;
    color: #004b84;
    font-weight: 600;
    letter-spacing: 0.0375rem;
    line-height: unset;
    padding: 0.3rem 0.6rem;
    transition: all 0.3s;
    text-transform: uppercase;
  }

  button.modal-button:hover {
    background-color: unset;
    cursor: pointer;
  }
  .modal-wrapper {
    display: grid;
    grid-template-columns: 0.85fr 1fr;
  }
  .dropdwn-selection {
    padding-top: 49px;
    max-width: 200px;
  }
</style>
