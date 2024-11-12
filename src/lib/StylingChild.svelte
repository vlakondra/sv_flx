<script>
    //Данные с определениями alignSelf-стиля
    import { alignSelfOptions } from "./select_values.svelte";
    let {activechild,event} = $props();
</script>

<div>
    {#if activechild.style}
        {activechild.id}
        <div class='select'>
            <select bind:value={activechild.style.alignSelf}
            onchange={()=>event()}>
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
                    bind:value={activechild.style.flexGrow}
                    onblur={()=>event()}
                    type="number"
                />
            </label>
        </div>
        <div class='input'>
            <label>
                order
                <input
                    bind:value={activechild.style.order}
                    onblur={()=>event()}
                    type="number"
                />
            </label>
        </div>
        <div class='input'>
            <label>
                flex-basic
                <input
                    bind:value={activechild.style.flexBasic}
                    onblur={()=>event()}
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
