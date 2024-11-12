<script>
  let { parentstyle,childstyle } = $props();
 
  let sk = ["{", "}"];
</script>

<div class='all-styles'>
  {JSON.stringify(parentstyle)}
  <!-- "Печатем" стили Parent'a.
   предусмотреть логику-->
  {#if parentstyle}
  <div>
    <div class='caption'>.parent {sk[0]}</div>
    <div>display: {parentstyle["display"]};</div>
    <div>flex-direction: {parentstyle["flex-direction"]};</div>
    <div>justify-content: {parentstyle["justify-content"]};</div>
    <div>{sk[1]}</div>
  </div>
  <div>
    Здесь разместить стили дочерних элементов,<br>
    предварительно создав их в App onStyleChange
    <div>test:{childstyle.test}</div>
  </div>
  {/if}
</div>




<style>
  .all-styles {
    background: aqua;
    margin-left: 2em;
    padding:10px;
  }
  .caption{
  font-weight: 600;
  }
  .caption ~ div{
    text-indent: 1em;
  }
</style>
