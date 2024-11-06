<script>
   let props =$props()

   const setColor=(ev)=>{
    props.activediv.style.background = ev.target.value
   }
</script>
<div>
    { props.activediv.style.background}
</div>
<div>
    <input value={props.activediv?   props.activediv.style.background:null} onblur={setColor} placeholder="background"/>
</div>