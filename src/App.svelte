<script>
  import FlexContainer from "./lib/FlexContainer.svelte";
  import StylingParent from "./lib/StylingParent.svelte";
  import StylingChild from "./lib/StylingChild.svelte";
  import PrintStyles from "./lib/PrintStyles.svelte";

  let isActive = $state(false);

  //Ссылка на DOM element с Flex-контейнером
  //будет получена из компонента FlexContainer и передана другим компонентам
  let flexContainerEl = $state();

  //при старте приложения в компонент StylingChild отправляется fake-объект с атрбутом style
  //поскольку активного child-объекта еще нет. Это нужно для инициализации компонента
  let activeChildEl = $state({ fake: 1, style: [1, 2, 3] });

  let actid = $state(-1);

  const actvateChild = (child_idx, sel_child) => {
    //устанавливает активный child
    isActive = true;
    actid = child_idx;
    activeChildEl = sel_child;
  };

  let parentstyle = $state();
  let childstyle = $state();
  function onStyleChange() {
    parentstyle = {
      display: flexContainerEl.style.display,
      "flex-direction": flexContainerEl.style.flexDirection,
      "justify-content": flexContainerEl.style.justifyContent,
    };
    childstyle = {
      test:123
    }
  }
</script>

<main>
  <div>
    <h1>START</h1>
    <div style="display: flex; flex-direction: row;">
      <div>
        <FlexContainer
          bind:flexContEl={flexContainerEl}
          activate={actvateChild}
        />
        <!-- <StylingParent container={flexContainerEl} /> -->

        <StylingParent event={onStyleChange} container={flexContainerEl} />

        <StylingChild event={onStyleChange} activechild={activeChildEl} isactive={isActive} />
      </div>
      <div>
        <PrintStyles {parentstyle} childstyle={childstyle} />
      </div>
    </div>
  </div>
</main>

<style>
  main {
    display: flex;
    justify-content: center;
  }
</style>
