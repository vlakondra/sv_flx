<script>
 import { getContext } from 'svelte';

 function rgbToHex(rgb) {
  // Extract red, green, and blue values from the RGB string
		if(!rgb)return
  const [r, g, b] = rgb.match(/\d+/g).map(Number);

  // Convert each red, green, and blue value to a hexadecimal string
  const hexR = r.toString(16).padStart(2, "0");
  const hexG = g.toString(16).padStart(2, "0");
  const hexB = b.toString(16).padStart(2, "0");

  // Combine the hexadecimal strings to form the final hex color string
  return `#${hexR}${hexG}${hexB}`;
}


let inp =$state()
const el = getContext('myKey');

$effect(()=>{
   inp.value = rgbToHex(el.pdiv().children[el.act()].style.background)
})

const onblur =(ev)=>{
    el.pdiv().children[el.act()].style.background = ev.target.value
}
</script>

<div>
   {el.act()} -- {el.pdiv()}

</div>
<input bind:this={inp} onblur={onblur} type='color'>