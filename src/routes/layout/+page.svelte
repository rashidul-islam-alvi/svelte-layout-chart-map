<script>
  import Mountain from "../../components/Mountain.svelte";
</script>

<div
  class="h-screen md:grid md:grid-cols-[repeat(12,1fr)] md:grid-rows-[repeat(6,1fr)] gap-x-0 gap-y-0"
>
  <div id="child-container" class="bg-blue-400 div1">
    3 x 2(color: blue-400)
  </div>
  <div id="child-container" class="bg-teal-400 div2">
    2 x 2(color: teal-400)
  </div>
  <div id="child-container" class="div3 bg-fuchsia-400">
    1 x 6(color:fuchsia-400)
  </div>
  <div id="child-container" class="div4 bg-rose-100">
    5 x 4(color: rose-100)
  </div>
  <div id="child-container" class="bg-blue-400 div5">
    2 x 6 (color: blue-400)
  </div>
  <div id="child-container" class="div6 bg-emerald-400">
    4 x 2 (color: emerald-400)
  </div>
  <div id="child-container" class="flex flex-col p-5 bg-yellow-100 div7">
    <span>4 x 4 (color: yellow-100)</span><Mountain />
  </div>
</div>

<style>
  #child-container {
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 500;
    font-size: 1.25rem;
  }

  @media only screen and (max-width: 768px) {
    #child-container {
      height: 50vh;
    }
  }

  .div1 {
    grid-area: 1 / 1 / 4 / 3;
  }
  .div2 {
    grid-area: 4 / 1 / 6 / 3;
  }
  .div3 {
    grid-area: 6 / 1 / 7 / 7;
  }
  .div4 {
    grid-area: 1 / 3 / 6 / 7;
  }
  .div5 {
    grid-area: 1 / 7 / 3 / 13;
  }
  .div6 {
    grid-area: 3 / 11 / 7 / 13;
  }
  .div7 {
    grid-area: 3 / 7 / 7 / 11;
  }
</style>
