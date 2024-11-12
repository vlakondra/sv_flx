<script>
    //Содержит flex-container c дочерними элементами
    //Позволяет изменять кол-во дочерних элементов
    //и устанавливать активный  элемент для установки индивидуальных стилей

    import { onMount } from "svelte";

    //Через flexContEl ссылка на flex-контейнер будет передана родителю (App).
    //Задействована руна $bindable
    let { flexContEl = $bindable(), ...props } = $props();

    //Кол-во дочерних элементов в флекс-контейнере по умолчанию
    let numDivs = $state(3);

    //Переменная flex_container связана с элементом div через директиву bind:this,
    //cодержащим отображаемый флекс-контейнер с его дочерними элементами
    let flex_container = $state();

    onMount(() => {
        //передаем ссылку на флекс-контейнер родителю (т.е. App)
        flexContEl = flex_container;
    });

    function setActive(idx, ev) {
        //снимаем признак активности у всех других дочерних элементов
        for (let el of flex_container.children) {
            el.style.background = null;
            el.id = "";
        }
        //устанавливаем активность у выбранного (по click) дочернего элемента
        ev.target.id = idx;
        ev.target.style.background = "yellow";

        //передаем активированный элемент родителю (т.е. в App)
        //через функцию activate (получена из App через props)
        props.activate(idx, ev.target);
    }

    const removeLastChild = () => {
        //удаляем последний дочерний элемент
        let l = flex_container.children.length;
        if (l == 1) return;

        let lastchild = flex_container.children[l - 1];

        // if (lastchild.id != "") {
        //    // props.deactivate();
        // }

        flex_container.removeChild(lastchild);
    };
</script>

<!-- svelte-ignore a11y_interactive_supports_focus -->
<!-- svelte-ignore a11y_click_events_have_key_events -->
<div bind:this={flex_container} class="flex-container">
    {#each [...Array(numDivs).keys()] as item, i}
        <div
            role="button"
            onclick={(event) => setActive(i, event)}
            class="flex-child"
        >
            <div class="child-label">{item + 1}</div>
        </div>
    {/each}
</div>

<div style='margin:10px 0'>
    <button onclick={() => numDivs++}>Добавить</button>
    <button onclick={removeLastChild}>Удалить</button>
</div>

<style>
    .flex-container {
        gap: 3px;
        min-width: 300px;
        max-width:400px;
        min-height: 200px;
        padding: 5px;
        border: 1px solid silver;
    }
    .flex-child {
        align-content: center;

        background: rgb(122, 122, 237);
        cursor: pointer;
    }
    .child-label {
        text-align: center;
        background: yellowgreen;
        width: 20px;
        margin: 20px;
    }
</style>
