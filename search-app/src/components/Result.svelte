<script>
  import { Query } from '@sveltestack/svelte-query';
  import Table from './Table.svelte';
  import { LightPaginationNav } from './pagination/index';
  import TableLoading from './TableLoading.svelte';
  import { cols, pages } from './store';
  import { col } from './SelectColumn';
  import Modal, { bind } from 'svelte-simple-modal';
  import { writable } from 'svelte/store';
  import Popup from './modal/Popup.svelte';
  const modal = writable(null);
  const showModal = () => modal.set(bind(Popup));

  const url = `https://www.callboxinc.com/wp-json/cbtk/v1/case-studies`;

  $: page = $pages;

  async function fetchPosts($pages) {
    // const data = await fetch(
    //   `${url}?s=tech&page=${page}&per_page=10&fields=${[5]}`
    // ).then((res) => res.json());
    // console.log(data);
    // return data;
    const res = await fetch(`${url}?s=tech&page=${page}&per_page=10&fields=5`);

    const data = await res.json();

    return data;
  }
  $: queryOptions = {
    queryKey: ['posts', page],
    queryFn: () => fetchPosts(page),
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
</script>

<div id="selection" class="modal">
  <Modal show={$modal}>
    <button class="modal-button" on:click={showModal}>Show modal</button>
  </Modal>
</div>

<Query options={queryOptions}>
  <div slot="query" let:queryResult={{ data, isFetching, isError }}>
    <div class="cntnr">
      <div class="results svelte-fhxlyi">
        {#if isFetching}
          <div class="loading">
            <div
              class="table-wrapper"
              class:tableScrolled={yTop > 45}
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
          <div class="area-2">
            <LightPaginationNav
              totalItems={data[0].total}
              pageSize={10}
              currentPage={$pages}
              limit={1}
              on:setPage={(e) => ($pages = e.detail.page)}
            />
          </div>

          <div
            class="table-wrapper"
            class:tableScrolled={yTop > 50}
            bind:this={box}
            on:scroll={parseScroll}
            on:mousemove={parseScroll}
          >
            <!-- this is table -->
            <Table tableData={data} tableheaderData={col} tableheader={$cols} />
            <!-- table helloworld -->
          </div>
        {/if}
      </div>
    </div>
  </div>
</Query>

<!-- 
<Query options={queryOptions}>
  <div slot="query" let:queryResult={{ data, isFetching, isError }}>
    <div class="cntnr">
      <div class="results svelte-fhxlyi">
        {#if isFetching}
          <h2>Loading...</h2>
        {:else if isError}
          <span>Error</span>
        {:else if data?.length}
          <h3>{data[0].label}</h3>
          {#if $selection > 0}
            <div class="area-4">
              <LightPaginationNav
                totalItems={data[0].total}
                pageSize={10}
                currentPage={page}
                limit={1}
                on:setPage={(e) => (page = e.detail.page)}
              />
            </div>
          {/if}
          <div
            class="table-wrapper"
            class:tableScrolled={yTop > 50}
            bind:this={box}
            on:scroll={parseScroll}
            on:mousemove={parseScroll}
          >
            <Table tableData={data} tableheaderData={col} tableheader={$cols} />
          </div>
        {/if}
      </div>
    </div>
  </div>
</Query> -->
<style>
  .table-wrapper {
    overflow: scroll;
    max-width: 1280px;
    max-height: 62vh;
    margin: 0 auto;
  }
  .loading {
    padding-top: 55px;
  }
  .modal {
    padding-left: 20px;
  }
  .modal-button {
    padding: 10px;
  }
  .cntnr {
    padding-top: 30px;
  }
  button.modal-button {
    background-color: #ffca09;
    border: 1px solid #ffca09;
    border-radius: 0.25rem;
    color: #004b84;
    font-weight: 600;
    letter-spacing: 0.0375rem;
    line-height: unset;
    padding: 0.75rem 1.25rem;
    transition: all 0.3s;
    text-transform: uppercase;
  }

  button.modal-button:hover {
    background-color: unset;
    cursor: pointer;
  }

  .area-2 {
    grid-column-start: 2;
    padding-left: 0;
    display: flex;
    justify-content: flex-end;
    padding: 10px;
  }
</style>
