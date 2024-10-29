<script>
  let display = $state([
    "block",
    "grid",
    "inline-block",
    "flex",
    "inline-flex",
    "none",
  ]);

  let flex_direction = $state([
    "row",
    "row-reverse",
    "column",
    "column-reverse",
  ]);

  let just_content = $state([
    "flex-start",
    "flex-end",
    "center",
    "space-between",
    "space-around",
  ]);

  let disp_selected = $state("block");
  let direct_selected = $state("row");
  let just_content_selected = $state("flex-start");

  import FlexShow from "./lib/FlexShow.svelte";
</script>

<main>
  <h1>START</h1>

  <div class="combos">
    <div>
      <select bind:value={disp_selected}>
        {#each display as item}
          <option>
            {item}
          </option>
        {/each}
      </select>
    </div>

    <div>
      <select bind:value={direct_selected}>
        {#each flex_direction as item}
          <option>
            {item}
          </option>
        {/each}
      </select>
    </div>

    <div>
      <select bind:value={just_content_selected}>
        {#each just_content as item}
          <option>
            {item}
          </option>
        {/each}
      </select>
    </div>

  </div>
<!-- Дочернему компоненту передаются значения props'ов и переменных стиля -->
  <div>
    <FlexShow
      --disp={disp_selected}
      --direct={direct_selected}
      --justcont ={just_content_selected}
      display={disp_selected}
      flex_dir={direct_selected}
      just_cont={just_content_selected}
    />
  </div>
</main>

<style>
  .combos {
    display: flex;
  }
  main{
    margin:auto;
    width:50%;
  }
</style>
