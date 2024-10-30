<script>
   import FlexShow from "./lib/FlexShow.svelte";

  //массивы для select'ов убрать в модуль и импортировать
  import { display  } from "./lib/select_values";
  import  {flex_direction} from "./lib/select_values";
  import {just_content} from "./lib/select_values"

  // let disp_selected = $state("block");
  // let direct_selected = $state("row");
  // let just_content_selected = $state("flex-start");

  // Объект для биндинга выбранных в select'ах значений
  let flexvals = $state({
    disp: "block",
    direct: "row",
    just_content: "flex-start",
  });

</script>

<main>
  <div>
    <h1>START</h1>

    <div class="combos">
      <div>
        <select bind:value={flexvals.disp}>
          {#each display as item}
            <option>
              {item}
            </option>
          {/each}
        </select>
      </div>

      <div>
        <select bind:value={flexvals.direct}>
          {#each flex_direction as item}
            <option>
              {item}
            </option>
          {/each}
        </select>
      </div>

      <div>
        <select bind:value={flexvals.just_content}>
          {#each just_content as item}
            <option>
              {item}
            </option>
          {/each}
        </select>
      </div>
    </div>

    <div>
      <!-- Оптимизация кода 1 -->
      <!-- <FlexShow
        --disp={disp_selected}
        --direct={direct_selected}
        --justcont={just_content_selected}
        display={disp_selected}
        flex_dir={direct_selected}
        just_cont={just_content_selected}
      
      <!-- Оптимизация кода 2 -->
      <!-- <FlexShow
      display={disp_selected}
      flex_dir={direct_selected}
      just_cont={just_content_selected}
    /> -->
      <!-- Оптимизация кода 3 -->
      <FlexShow selected={flexvals} />
    </div>
  </div>
</main>

<style>
  .combos {
    display: flex;
  }
  main {
    display: flex;
    justify-content: center;
  }
</style>
