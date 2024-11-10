<script>
    //Данные с определениями alignSelf-стиля
    import { alignSelfOptions } from "./select_values.svelte";
    let props = $props();
</script>

<div>
    {#if props.activechild.style}
        {props.activechild.id}
        <div class='select'>
            <select bind:value={props.activechild.style.alignSelf}>
                <option value="" selected disabled
                    >Индивидуальное выравнивание</option
                >
                {#each alignSelfOptions.alignSelf as item}
                    <option value={item}>
                        {item}
                    </option>
                {/each}
            </select>
        </div>
        <div class='input'>
            <label>
                flex-grow
                <input
                    bind:value={props.activechild.style.flexGrow}
                    type="number"
                />
            </label>
        </div>
        <div class='input'>
            <label>
                order
                <input
                    bind:value={props.activechild.style.order}
                    type="number"
                />
            </label>
        </div>
        <div class='input'>
            <label>
                flex-basic
                <input
                    bind:value={props.activechild.style.flexBasic}
                    type="text"
                />
            </label>
        </div>
    {/if}
</div>


<style>
    label {
        width:80px;
        display: block;
    }
    .select,.input{
        margin-bottom: 10px;
    }
</style>
