<script>
     let props = $props();

    import { display  } from "./select_values.svelte";
    import  {flex_direction} from "./select_values.svelte";
    import {just_content} from "./select_values.svelte"

  let flexvals = $state({
    disp: "block",
    direct: "row",
    just_content: "flex-start",
  });



const onChangeDisplay=(ev)=>{
    props.container.style.display=flexvals.disp
}
const onChangeDirect=(ev)=>{
    props.container.style.flexDirection=flexvals.direct
}
const onChangeJustContent=(ev)=>{
    props.container.style.justifyContent= ev.target.value//flexvals.just_content
}


</script>

<div class="combos">
    <div>
      <select bind:value={flexvals.disp} onchange="{onChangeDisplay}">
        {#each display as item}
          <option value={item}>
            {item}
          </option>
        {/each}
      </select>
    </div>

    <div>
        <select bind:value={flexvals.direct} onchange={onChangeDirect}>
          {#each flex_direction as item}
            <option value={item}>
              {item}
            </option>
          {/each}
        </select>
      </div>

      <div>
        <select bind:value={flexvals.just_content} onchange={onChangeJustContent}>
          {#each just_content as item}
            <option value={item}>
              {item}
            </option>
          {/each}
        </select>
      </div>
    </div>



    

<style>
    .combos {
      display: flex;
    }
</style>