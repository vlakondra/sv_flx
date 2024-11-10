<script>
    let props = $props();

    const addDiv=()=>{
        let el = document.createElement("div")
        el.textContent='555'
        props.container.appendChild(el)
    }
</script>

<div>
    <button onclick={addDiv}>Add Child Div</button>
</div>