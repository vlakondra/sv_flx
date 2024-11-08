<script>
   let props =$props()

   const setColor=(ev)=>{
    props.activediv.style.background = ev.target.value
   }
</script>
<div>
    {#if props.activediv}
         { props.activediv.style.background}
    {/if}
</div>
<div>
    <!-- При открытии активного div'a нет!!! -->
    <input value={props.activediv?   props.activediv.style.background : null} onblur={setColor} placeholder="background"/>
</div>