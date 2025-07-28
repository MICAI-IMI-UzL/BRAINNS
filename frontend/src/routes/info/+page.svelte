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
    <div>
      {#if userGuideHtml}
          <div class="markdown">{@html userGuideHtml}</div>
      {:else}
          <p>Lade Benutzerhandbuch…</p>
      {/if}
    </div>
</PageWrapper>

<style global>
  /* Optionales Styling für Markdown */
  :global(.markdown) {
    max-width: 1000px;
    margin: 2rem auto;
    /* ... rest siehe oben */
  }
  :global(.markdown a) {
    color: var(--button-color-bright-blue);
    /* ... */
  }

  .markdown a:hover,
  .markdown a:focus {
    color: var(--button-color-bright-green);
    text-decoration: none;
  }

  /* Optional: Überschriften zentrieren */
  .markdown h1,
  .markdown h2,
  .markdown h3 {
    text-align: center;
    margin-top: 2rem;
    margin-bottom: 1rem;
  }
</style>