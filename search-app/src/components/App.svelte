<script>
  import ViewResult from './ViewResult.svelte';
  import SearchResult from './SearchResult.svelte';
  import Result from './Result.svelte';
  import { QueryClient, QueryClientProvider } from '@sveltestack/svelte-query';
  import { isSearching, fields, seeMore, MoreField, viewfield } from './store';
  import SearchForm from './SearchForm.svelte';
  import FieldResult from './FieldResult.svelte';
  import SeeMore from './SeeMore.svelte';
  import MoreFieldResult from './MoreFieldResult.svelte';

  const queryClient = new QueryClient();
</script>

<QueryClientProvider client={queryClient}>
  <div>
    {#if $isSearching}
      {#if $fields.length}
        <FieldResult />
      {:else}
        <SearchResult />
      {/if}
    {:else if $viewfield}
      <ViewResult />
    {:else if $MoreField}
      <MoreFieldResult />
    {:else if $seeMore}
      <SeeMore />
    {:else}
      <SearchForm />

      <Result />
    {/if}
  </div>
</QueryClientProvider>

<style lang="scss">
  @use '../styles/app';

  @include app.reset;

  @include app.root {
    main {
      text-align: center;
      padding: 1rem;
      max-width: 240px;
      margin: 0 auto;

      @include app.screen-sm {
        max-width: none;
      }
    }

    h1 {
      color: app.$colors-blue-400;
      text-transform: uppercase;
      font-size: 3.75rem;
      line-height: 1;
    }
  }
</style>
