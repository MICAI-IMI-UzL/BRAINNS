<script>
    import PageWrapper from "../../single-components/PageWrapper.svelte";
    import { onMount } from 'svelte';
    import { marked } from 'marked';

    let userGuideHtml = '';

    onMount(async () => {
        try {
            const res = await fetch('/brainns/User-Guides-de.md');
            console.log('Fetch Response:', res);

            if (!res.ok) {
                throw new Error(`Fehler beim Laden der Datei: ${res.status}`);
            }

            const markdown = await res.text();
            console.log('Markdown-Inhalt:', markdown.slice(0, 200)); // nur ein Ausschnitt

            userGuideHtml = marked.parse(markdown);
        } catch (error) {
            console.error('Fehler beim Laden des Benutzerhandbuchs:', error);
        }
    });
</script>

<PageWrapper>
  <div class="card">
    <div>
      {#if userGuideHtml}
          <div class="markdown">{@html userGuideHtml}</div>
      {:else}
          <p>Lade Benutzerhandbuch…</p>
      {/if}
    </div>
  </div>
</PageWrapper>

<style global>
  /* Optionales Styling für Markdown */
  :global(.markdown) {
    margin: 2rem auto;
    /* ... rest siehe oben */
  }
  :global(.markdown a) {
    color: var(--button-color-bright-blue);
    /* ... */
  }

  :global(.markdown a:hover),
  :global(.markdown a:focus) {
    color: var(--button-color-bright-green);
    text-decoration: none;
  }

  /* Optional: Überschriften zentrieren */
  :global(.markdown h1),
  :global(.markdown h2),
  :global(.markdown h3) {
    margin-top: 2rem;
    margin-bottom: 1rem;
  }

  :global(.markdown img) {
    max-width: 100%;
    height: auto;
    display: block;
    margin: 0 auto;
  }

  .card {
    background: #1f2937;
    border-radius: 12px;
    padding: 1.5rem;
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    max-width: 1000px;
    margin: 0 auto;
  }
</style>