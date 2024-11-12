<script>
  //Компонет для определения flex-стилей контейнера посредством шести select'ов.
  //Ссылка на контейнер формируется в компоненте FlexContainer и передается сюда
  // в качестве props из корневого компнента App

  import { onMount } from "svelte";
  let { container, event } = $props();

  //Данные с определениями flex-стилей
  import { flexOptions } from "./select_values.svelte";

  onMount(() => {
    //берем 1-е элементы из массивов объекта flexOptions и определяем стили контейнера.
    //Нужно проверить, чтобы они соответствовали значениям по умолчанию.
    // props.container.style.display = flexOptions.display[0];
    // props.container.style.flexDirection = flexOptions.flexDirection[0];
    // props.container.style.justifyContent = flexOptions.justifyContent[0];
    // props.container.style.alignItems = flexOptions.alignItems[0];
    // props.container.style.flexWrap = flexOptions.flexWrap[0];
    // props.container.style.alignContent = flexOptions.alignContent[0];

    container.style.display = flexOptions.display[0];
    container.style.flexDirection = flexOptions.flexDirection[0];
    container.style.justifyContent = flexOptions.justifyContent[0];
    container.style.alignItems = flexOptions.alignItems[0];
    container.style.flexWrap = flexOptions.flexWrap[0];
    container.style.alignContent = flexOptions.alignContent[0];
  });

  const setStyles = (ev) => {
    //value select'ов содержит название css-свойства и его значение через запятую.
    //поэтому их нужно разделить и присвоить соответствующим css-свойствам контейнера.
    let spl = ev.target.value.split(",");
    // props.container.style[spl[0]] = spl[1];
    container.style[spl[0]] = spl[1];
    //++ после изменения стиля вызываем событие, к-е 
    //будет обрабатываться в App
    event();
  };

  const setCaption = (atr) => {
    //Формируем заголовки как в CSS, а не в JS
    switch (atr) {
      case "display":
        return atr + ": ";
      case "flexDirection":
        return "flex-direction" + ": ";
      //закончить!!!
      default:
        return atr;
    }
  };
</script>

<!-- все select'ы строятся из коллекции flexOptions -->
<div class="style-controls">
  {#each Object.keys(flexOptions) as key, i}
    <div class="selects">
      <div class="caption-select">
        <div>{setCaption(key)}</div>

        <select onchange={setStyles}>
          {#each flexOptions[key] as val}
            <option value={key + "," + val}>{val}</option>
          {/each}
        </select>
      </div>
    </div>
  {/each}
</div>

<!--ЛИКВИДАЦИЯ 6 select'ов <div class="combos">
  <div>
    <select bind:value={flexvals.display} onchange={onChangeDisplay}>
      {#each flexOptions.display as item}
        <option value={item}>
          {item}
        </option>
      {/each}
    </select>
  </div>

  <div>
    <select bind:value={flexvals.direct} onchange={onChangeDirect}>
      {#each flexOptions.flexDirection as item}
        <option value={item}>
          {item}
        </option>
      {/each}
    </select>
  </div>

  <div>
    <select bind:value={flexvals.just_content} onchange={onChangeJustContent}>
      {#each flexOptions.justifyContent as item}
        <option value={item}>
          {item}
        </option>
      {/each}
    </select>
  </div>
</div> -->

<style>
  .style-controls {
    display: flex;
    flex-direction: column;
  }
  .selects {
    display: flex;
    flex-direction: column;
  }
  .caption-select {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  select {
    width: 150px;
  }
</style>
