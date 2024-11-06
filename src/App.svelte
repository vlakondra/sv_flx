<script>
  import { onMount } from "svelte";
  import FlexShow from "./lib/FlexShow.svelte";
  import EditChilds from "./lib/EditChilds.svelte";
  import EditParent from "./lib/EditParent.svelte";

  import DemoFlex from "./lib/DemoFlex.svelte";
  import FlexChildStyling from "./lib/FlexChildStyle.svelte";

  //массивы для select'ов убрать в модуль и импортировать
  import { display } from "./lib/select_values.svelte";
  import { flex_direction } from "./lib/select_values.svelte";
  import { just_content } from "./lib/select_values.svelte";

  let flex_container = $state();

  //Ссылка на DOM element с Flex-контейнером
  //будет получена из компонента DemoFlex и передана другим компонентам
  let demoflex_El = $state({});


  let activeChild =$state()
  // let disp_selected = $state("block");
  // let direct_selected = $state("row");
  // let just_content_selected = $state("flex-start");

  // Объект для биндинга выбранных в select'ах значений
  let flexvals = $state({
    disp: "block",
    direct: "row",
    just_content: "flex-start",
  });

  const actvateChild = (sel_child)=>{
    activeChild = sel_child
    console.log(activeChild)
  }
</script>

<main>
  <div>
    <h1>START</h1>

    <DemoFlex bind:demoflexel={demoflex_El} activate={actvateChild} />
    <EditChilds container={demoflex_El} />
    <EditParent container={demoflex_El} />
    <FlexChildStyling activediv = {activeChild}/>



    <div bind:this={flex_container}>
      <div>7</div>
      <div>8</div>
      <div>9</div>
    </div>

    <!-- перенести это в компонент -->
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

    <FlexShow selected={flexvals} />
  </div>
</main>

<style>
  .flexshow {
    display: var(--disp);
    flex-direction: var(--direct);
    justify-content: var(--justcont);
    border: 1px solid silver;
    width: 318px;
  }

  .combos {
    display: flex;
  }
  main {
    display: flex;
    justify-content: center;
  }
</style>
