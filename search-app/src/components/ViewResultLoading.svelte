<script>
  import Skeleton from 'svelte-skeleton/Skeleton.svelte';
</script>

<div class="results svelte-fhxlyi">
  <div class="cs-hero">
    <div class="client-success-story">client success story</div>
  </div>
  <div class="container">
    <div class="case-study-outer">
      <article class="post">
        <section class="cs-entry">
          <div>
            <Skeleton height="240" width="400" secondaryColor="#f5f4f4" />
          </div>
          <div class="entry-outer">
            <header>
              <h1 class="cs-title">
                <Skeleton height="35" width="400" secondaryColor="#f5f4f4" />
                <Skeleton height="35" width="395" secondaryColor="#f5f4f4" />
                <Skeleton height="35" width="340" secondaryColor="#f5f4f4" />
              </h1>
            </header>
            <footer>
              <Skeleton height="57" width="200" secondaryColor="#f5f4f4" />
            </footer>
          </div>
        </section>
        <div class="cs-results">
          <Skeleton height="180" width="300" secondaryColor="#f5f4f4" />
          <Skeleton height="180" width="300" secondaryColor="#f5f4f4" />
          <Skeleton height="180" width="300" secondaryColor="#f5f4f4" />
          <Skeleton height="180" width="300" secondaryColor="#f5f4f4" />
        </div>
        <div class="cs-campaign">
          <div class="cs-specs">
            <div>
              <span class="fa fa-briefcase" />
              <div class="cs-specs-label">Industry</div>
              <div class="cs-specs-post">
                <Skeleton height="25" width="100" secondaryColor="#f5f4f4" />
              </div>
            </div>
            <div>
              <span class="fa fa-map-marker-alt" />
              <div class="cs-specs-label">Location</div>
              <div class="cs-specs-post">
                <Skeleton height="25" width="70" secondaryColor="#f5f4f4" />
              </div>
            </div>
            <div>
              <span class="fa fa-building" />
              <div class="cs-specs-label">Headquarters</div>
              <div class="cs-specs-post">
                <Skeleton height="25" width="80" secondaryColor="#f5f4f4" />
              </div>
            </div>
            <div>
              <span class="fa fa-chart-line" />
              <div class="cs-specs-label">Campaign Type</div>

              <div>
                <div class="cs-specs-post">
                  <Skeleton height="25" width="90" secondaryColor="#f5f4f4" />
                </div>
              </div>
            </div>
            <div>
              <span class="fa fa-map-marker-alt" />
              <div class="cs-specs-label">Target Location</div>
              <div class="cs-specs-post">
                <Skeleton height="25" width="80" secondaryColor="#f5f4f4" />
              </div>
            </div>
            <div>
              <span class="fa fa-briefcase" />
              <div class="cs-specs-label">Target Industries</div>
              <div class="cs-specs-post">
                <Skeleton height="50" width="90" secondaryColor="#f5f4f4" />
              </div>
            </div>
            <div>
              <span class="fa fa-user" />
              <div class="cs-specs-label">Target Contacts</div>
              <div class="cs-specs-post">
                <Skeleton height="70" width="100" secondaryColor="#f5f4f4" />
              </div>
            </div>
          </div>
        </div>
      </article>
    </div>
  </div>
</div>

<style>
  h2 {
    font-family: 'Work Sans', work-sans, sans-serif;
    font-weight: 700;
    margin: 0;
    padding: 0;
    color: #014e89;
  }
  img {
    display: block;
    width: 100%;
    height: auto;
  }
  .cs-content {
    display: grid;
    row-gap: 3rem;
  }
  .cs-campaign {
    display: grid;
    row-gap: 3rem;
  }
  .cs-specs-label {
    font-family: 'Work Sans', work-sans, sans-serif;
    font-weight: 700;
    color: #5f7380;
    margin: 0.25rem 0;
  }
  .cs-specs-post {
    font-size: 0.975rem;
    line-height: 1.5rem;
    font-family: 'Lato', sans-serif;
    font-weight: 400;
    color: #5f7380;
  }
  .cs-highlights {
    padding: 1.5rem;
    border: 1px solid #f76823;
    border-radius: 0.875rem;
    width: auto;
    margin-left: 0;
    background-color: rgba(247, 104, 35, 0.07);
  }
  .cs-specs {
    grid-template-columns: 1fr 1fr 1fr 1fr;
    display: grid;

    gap: 1rem;
    font-size: 0.875rem;
    line-height: 1.25rem;
  }
  .entry-outer {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
  }
  .cs-title {
    color: #014e89;
    font-size: 1.875rem;
    line-height: 2.25rem;
    margin: 0 0 2rem;
  }
  .pdf-button {
    display: inline-block;
    width: auto;
    padding: 1rem 1.25rem;
    font-size: 1rem;
    line-height: 1.5rem;
    font-family: 'Work Sans', work-sans, sans-serif;
    font-weight: 600;
    text-align: center;
    text-decoration: none;
    background-color: #ffca09;
    color: #014e89;
    border-radius: 0.25rem;
    box-shadow: 0px 8px 9px -6px rgb(95 115 128 / 44%);
    cursor: pointer;
    transition: all 300ms ease 0ms;
    font-size: 1.125rem;
    line-height: 1.75rem;
    font-family: 'Work Sans', work-sans, sans-serif;
    background-color: #fa450e;
    color: #fff;
    border-color: unset;
    outline: 0;
    max-width: 100%;
  }
  .pdf-button:hover {
    color: #fff;
    text-decoration: none;
    box-shadow: 0px 13px 9px -6px rgb(95 115 128 / 44%);
    transform: translateX(0px) translateY(-5px);
  }
  .cs-results {
    grid-template-columns: 1fr 1fr 1fr;
    gap: 1.5rem;
    display: grid;
  }
  .cs-result {
    padding: 2rem;
    border: 1px solid #14b37d;
    border-radius: 0.875rem;
    color: #14b37d;
    text-align: center;
    transition: background-color 0.3s linear;
    display: grid;
    row-gap: 0.375rem;
    align-content: center;
  }
  .cs-result-label {
    font-size: 1.5rem;
    line-height: 2rem;
  }
  .cs-result-value {
    font-size: 2.25rem;
    line-height: 2.5rem;
  }
  .cs-entry {
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    display: grid;
  }
  .cs-hero {
    height: 40vh;
    padding: calc(15vh / 2 - 1.125rem) 0 0;
    letter-spacing: 0.05em;
    background-color: #063060;
  }
  .client-success-story {
    font-size: 2.25rem;
    line-height: 2.5rem;
    font-family: 'Work Sans', work-sans, sans-serif;
    font-weight: 700;
    color: #ffca09;
    text-align: center;
    text-transform: capitalize;
    letter-spacing: 0.05em;
    margin: 0;
  }
  .case-study-outer {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
  }
  .post {
    padding: 3rem;
    background-color: #fff;
    border-radius: 0.875rem;
    position: relative;
    top: -25vh;
    display: grid;
    row-gap: 3rem;
  }
  .container {
    padding-right: calc(1280px / 12);
    padding-left: calc(1280px / 12);
  }
</style>
