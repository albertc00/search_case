<script>
  import { Query } from '@sveltestack/svelte-query';
  import NoResult from './NoResult.svelte';
  import SearchFormClose from './SearchFormClose.svelte';
  import { fields, isSearching, SearchTerm, seeMore } from './store';

  const url = `https://www.callboxinc.com/wp-json/cbtk/v1/case-studies`;
  let page = 1;
  let s;
  $: s = $SearchTerm.toLowerCase();
  $: field = $fields;
  async function fetchPosts(page = 1, s) {
    const data = await fetch(`${url}?s=${s}&page=${page}&per_page=10
      `).then((res) => res.json());

    return data;
  }
  $: queryOptions = {
    queryKey: ['posts', page, s],
    queryFn: () => fetchPosts(page, s),
    keepPreviousData: true,
    staleTime: Infinity,
    cacheTime: 1000 * 60 * 5,
  };

  function onClick(value) {
    $seeMore = true;
    $isSearching = false;
    $SearchTerm = s;
    $fields = value;
  }
</script>

<SearchFormClose />

<Query options={queryOptions}>
  <div slot="query" let:queryResult>
    <div class="cntnr svelte-y5n953">
      <div class="results svelte-14s95pw ">
        {#if queryResult.isFetching}
          <h2>Loading...</h2>
        {:else if queryResult.error}
          <span>Error</span>
        {:else if queryResult.data?.length}
          {#each queryResult.data as { n, id, label, icon, posts, hasMore } (id)}
            <div class="table-wrapper">
              <h4 class="table-label">{label}</h4>
              <table>
                <thead>
                  <tr>
                    <th>id</th>
                    <th>Title</th>
                    <th>Web Page</th>
                  </tr>
                </thead>

                <tbody>
                  {#each posts as post (post.id)}
                    <tr>
                      <td>{post.id}</td>
                      <td>{post.title}</td>
                      <td>{post.link}</td>
                    </tr>
                  {/each}
                </tbody>
              </table>
              {#if hasMore}
                <div class="seeAll svelte-14s95pw">
                  <button
                    type="button"
                    class="link svelte-1yo2ena primary"
                    aria-label="See all results for Title"
                    on:click={() => onClick(n)}>See all »</button
                  >
                </div>
              {:else}
                <button
                  type="button"
                  class="link svelte-1yo2ena primary"
                  aria-label="See all results for Title"
                  on:click={() => onClick(n)}>View »</button
                >
              {/if}
            </div>
          {/each}
        {:else}
          <NoResult />
        {/if}
      </div>
    </div>
  </div>
</Query>

<style>
  table,
  td {
    border: 1px solid;
    border-collapse: collapse;
    margin-bottom: 10px;
    padding: 10px;
  }
  th {
    color: #014e89;
    border: 1px solid;
    border-collapse: collapse;
    margin-bottom: 10px;
    padding: 10px;
  }
  tr:nth-child(even) {
    background-color: #dbdada;
  }
  .table-wrapper {
    padding: 1.5rem;
  }
  .table-label {
    padding: 5px;
    font-family: 'Work Sans', work-sans, sans-serif;
    font-size: 1.5rem;
    font-weight: 600;
    line-height: 2rem;
    color: #231f20;
  }
</style>
