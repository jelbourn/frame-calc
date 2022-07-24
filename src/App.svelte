<script lang="ts">
  // Default to 8x11
  let pictureWidth = 8;
  let pictureHeight = 11;

  // Default to 3/8 rabbet
  let rabbetDepth = 0.375;

  // Default to frame width of 1.5
  let frameThickness = 1.5;

  let scale = 5;

  // Dimensions to cut (before miters)
  $: cutWidth = (2 * frameThickness) + pictureWidth - (2 * rabbetDepth);
  $: cutHeight = (2 * frameThickness) + pictureHeight - (2 * rabbetDepth);

  // Inner dimensions for reference only
  $: innerWidth = pictureWidth - (2 * rabbetDepth);
  $: innerHeight = pictureHeight - (2 * rabbetDepth);

  $: rabbetCorner = frameThickness - rabbetDepth;
</script>

<form>
  <label>Picture width <input type="number" bind:value="{pictureWidth}"></label>
  <label>Picture height <input type="number" bind:value="{pictureHeight}"></label>
  <label>Rabbet depth <input type="number" bind:value="{rabbetDepth}"></label>
  <label>Frame thickness <input type="number" bind:value="{frameThickness}"></label>
  <label>Scale <input type="range" min="1" max="8" bind:value="{scale}"></label>
  <span>Cut width: {cutWidth}</span>
  <span>Cut height: {cutHeight}</span>
  <span>Inner width: {innerWidth}</span>
  <span>Inner height: {innerHeight}</span>
</form>

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" preserveAspectRatio="" style="width: 800px; height: 800px;">
  <polygon id="top" points="0,0 {cutWidth * scale},0 {(cutWidth - frameThickness) * scale},{frameThickness * scale} {frameThickness * scale},{frameThickness * scale}"/>
  <polygon id="left" points="0,0 0,{cutHeight * scale} {frameThickness * scale},{(cutHeight - frameThickness) * scale} {frameThickness * scale},{frameThickness * scale}"></polygon>
  <polygon id="bottom" points="0,{cutHeight * scale} {frameThickness * scale},{(cutHeight - frameThickness) * scale} {(cutWidth - frameThickness) * scale},{(cutHeight - frameThickness) * scale} {cutWidth * scale},{cutHeight * scale}"></polygon>
  <polygon id="right" points="{cutWidth * scale},{cutHeight * scale} {cutWidth * scale},0 {(cutWidth - frameThickness) * scale},{frameThickness * scale} {(cutWidth - frameThickness) * scale},{(cutHeight - frameThickness) * scale}"></polygon>

  <polygon id="rabbet" stroke-width="0.25" stroke-dasharray="2 0.5" points="{rabbetCorner * scale},{rabbetCorner * scale} {rabbetCorner * scale},{(frameThickness + innerHeight + rabbetDepth) * scale} {(rabbetDepth + innerWidth + frameThickness) * scale},{(frameThickness + innerHeight + rabbetDepth) * scale} {(rabbetDepth + innerWidth + frameThickness) * scale},{rabbetCorner * scale}"></polygon>
</svg>

<style>
  form {
    display: inline-flex;
    flex-direction: column;

    border: 2px solid #535bf2;
    border-radius: 8px;
    padding: 8px;
    margin: 16px;
    text-align: right;
  }

  svg {
    fill: rosybrown;
    stroke: none;
    margin: 16px;
  }

  #rabbet {
    fill: transparent;
    stroke: ghostwhite;
  }

  input {
    width: 175px;
  }
</style>
