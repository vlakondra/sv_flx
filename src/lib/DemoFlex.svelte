<script>
//Формирует ссылку на родит-й контейнер, изменяет кол-во дочерних эл-в и
//устанавливает активный

    import { onMount } from "svelte";
    let { demoflexel = $bindable(), ...props } = $props();

    let numDivs = $state(3);

    let flex_container = $state();

    onMount(() => {
        console.log("Mounting...", flex_container);
        demoflexel = flex_container;

        console.log(props.test);
    });

    function setActive(ev) {
        //снимаем признак активности
        for (let el of flex_container.children) {
            el.style.background = null;
        }
       // ev.target.style.background = "yellow";
        //установка активного Div'a
        //?? props.activeDiv = null
        props.activate(ev.target);
    }


</script>

<!-- svelte-ignore a11y_interactive_supports_focus -->
<!-- svelte-ignore a11y_click_events_have_key_events -->
<div bind:this={flex_container}>
    {#each [...Array(numDivs).keys()] as item}
        <div role="button" onclick={setActive}>{item}</div>
    {/each}
</div>
<div>
    <!-- При удалении активного div'а activeDiv не обнуляется!!! -->
    <button onclick={() => numDivs++}>+</button>
    <button onclick={() =>  {props.deact(); numDivs--}}>-</button>
</div>

<style>
    div div {
        cursor: pointer;
    }
</style>
