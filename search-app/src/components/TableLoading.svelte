<script>
  import Skeleton from 'svelte-skeleton/Skeleton.svelte';

  // function* iter_range(begin, end, step) {
  //   // Normalize our inputs
  //   step = step ? step : 1;

  //   if (typeof end === 'undefined') {
  //     end = begin > 0 ? begin : 0;
  //     begin = begin < 0 ? begin : 0;
  //   }

  //   if (begin == end) {
  //     return;
  //   }

  //   if (begin > end) {
  //     step = step * -1;
  //   }

  //   for (let x = begin; x < end; x += step) {
  //     yield x;
  //   }
  // }

  // export function range(begin, end, step) {
  //   return Array.from(iter_range(begin, end, step));
  // }
  // let begin = 0;
  // let end = 10;
  // let step = 1;
  const loading = [575, 490, 530, 528, 562, 524, 500, 500, 500, 500];
</script>

<table>
  <thead>
    <tr>
      <th> Title </th>
      <!-- <th> Status </th>
      <th> Excerpt </th>
      <th> image </th> -->
    </tr>
  </thead>
  <tbody>
    <!-- {#each range(begin, end, step) as i} -->
    {#each loading as load}
      <tr>
        <td><Skeleton height="25" width={load} /> </td>
      </tr>
    {/each}
    <!-- {/each} -->
  </tbody>
</table>

<style>
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
</style>
