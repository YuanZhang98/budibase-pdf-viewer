<script>
  import { getContext } from "svelte"

  const { styleable } = getContext("sdk")
  const component = getContext("component")
  export let dataProvider;

  $: file = dataProvider?.rows?.map((obj) => ({
    name: obj.FileName,
    fileData: obj.Pdf[0].url
  })) ?? [];
</script>

<div use:styleable={$component.styles}>
  {#each file as pdfFile (pdfFile)}
    {#if pdfFile.name && pdfFile.fileData}
        <iframe
                src={pdfFile.fileData}
                width=500
                height=680
        >
        </iframe>
      {/if}
    {/each}
</div>