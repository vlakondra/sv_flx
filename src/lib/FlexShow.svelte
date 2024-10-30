<script>
  let props = $props();

  //вызывается при изменении любого props'a
  //и обновляет значения массива для распечатки стиля
  $effect(() => {
    // console.log(props.selected)
    //!! $inspect(props.selected);

    stl.display = props.selected.disp;
    stl["flex-direction"] = props.selected.direct;
    stl["justify-content"] = props.selected.just_content;
  });

  //объект для распечатки стиля с умолчаниями
  let stl = $state({
    display: "block",
    "flex-direction": "row",
    "justify-content": "flex-start",
  });

  //имя класса для распечатки стиля
  let class_name = ".flex-class {";
</script>

<div
  style="--disp:{props.selected.disp};
         --direct:{props.selected.direct};
         --justcont:{props.selected.just_content}"
>
  <div class="flex-show">
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </div>

  <div class="print-style">
    <div>{@html class_name}</div>
    <!-- Печатаем стили -->
    {#each Object.keys(stl) as item, i}
      <div>{item}:{stl[item]}</div>
    {/each}

    <div>}</div>
  </div>
</div>

<style>
  .flex-show {
    display: var(--disp);
    flex-direction: var(--direct);
    justify-content: var(--justcont);
    border: 1px solid silver;
    width: 318px;
  }
  .print-style {
    border: 1px solid silver;
    width: 200px;
    padding: 20px;
    margin-top: 20px;
    background-color: aqua;
  }
</style>
