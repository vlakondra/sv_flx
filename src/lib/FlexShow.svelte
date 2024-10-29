<script>
  let props = $props();

  //вызывается при изменении любого props'a 
  //и обновляет значения массива для распечатки стиля
  $effect(() => {
    stl.display = props.display;
    stl["flex-direction"] = props.flex_dir;
    stl["justify-content"] = props.just_cont;
  });

  //массив для распечатки стиля с умолчаниями
  let stl = $state({
    "display": "flex",
    "flex-direction": "row",
    "justify-content": "flex-start",
  });

  //имя сласса для распечатки стиля
  let class_name = ".flex-class {";
</script>

<div>
  <div class="flex-show">
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </div>

  <div class="print-style">
    <div>{@html class_name}</div>
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
    margin-top: 20px;;
    background-color: aqua;
  }
</style>
