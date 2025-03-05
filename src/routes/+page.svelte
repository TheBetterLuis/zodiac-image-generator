<script>
  import {
    mdiZodiacScorpio,
    mdiZodiacAquarius,
    mdiZodiacAries,
    mdiZodiacCancer,
    mdiZodiacCapricorn,
    mdiZodiacPisces,
    mdiZodiacLeo,
    mdiZodiacLibra,
    mdiZodiacGemini,
    mdiZodiacSagittarius,
    mdiZodiacTaurus,
    mdiZodiacVirgo,
  } from '@mdi/js';
import html2canvas from 'html2canvas';
 
  function handleIconChange(event) {
    selectedIcon = icons[event.target.value];
  }

  let backgroundImageSrc = null;
  async function handleBackgroundImageChange(event) {
    const file = event.target.files[0];
    if (file) {
      backgroundImageSrc = URL.createObjectURL(file);
    }
  }

  function downloadImage() {
    const downloadDiv = document.getElementById('download-div');
    if (!downloadDiv) return;

    html2canvas(downloadDiv, { scale: 3 }).then(canvas => {
      const link = document.createElement('a');
      link.href = canvas.toDataURL('image/png');
      link.download = `${zodiacName}.png`;
      link.click();
    });
  }

  let iconSize = 100;
  let iconColor = 'red';
  let igColor = 'green';
  /*
  const colors = [
    'red', 'blue', 'green', 'yellow', 'black', 'white', // Add more colors as needed
  ];
  */
const colors = [
  'red', 'blue', 'green', 'yellow', 'black', 'white',
  'orange', 'purple', 'pink', 'brown', 'gray', 'cyan',
  'magenta', 'lime', 'teal', 'maroon', 'navy', 'olive',
  'silver', 'gold', 'coral', 'violet', 'indigo', 'salmon',
  'tomato', 'steelblue', 'skyblue', 'sienna', 'seashell',
  'seagreen', 'royalblue', 'rosybrown', 'rebeccapurple', 'orchid',
  'mediumvioletred', 'mediumturquoise', 'mediumspringgreen',
  'mediumslateblue', 'mediumseagreen', 'mediumorchid',
  'mediumblue', 'lightskyblue', 'lightsalmon', 'lightseagreen',
  'lightsteelblue', 'lightslategray', 'lightgreen', 'lightcoral',
  'lightblue', 'lemonchiffon', 'lavenderblush', 'lavender',
  'khaki', 'ivory', 'honeydew', 'hotpink', 'gainsboro',
  'fuchsia', 'forestgreen', 'floralwhite', 'firebrick',
  'darkviolet', 'darkturquoise', 'darkslateblue', 'darkseagreen',
  'darkred', 'darkorchid', 'darkmagenta', 'darkkhaki',
  'darkgreen', 'darkgray', 'darkgoldenrod', 'darkcyan',
  'darkblue', 'crimson', 'cornsilk', 'cornflowerblue',
  'chocolate', 'chartreuse', 'cadetblue', 'burlywood',
  'blueviolet', 'blanchedalmond', 'beige', 'azure', 'aquamarine',
  'antiquewhite', 'aliceblue',
];
 let zodiacName = 'Escorpio';
  const icons = {
    Escorpio: mdiZodiacScorpio,
    Acuario: mdiZodiacAquarius,
    Aries: mdiZodiacAries,
    Cancer: mdiZodiacCancer,
    Capricornio: mdiZodiacCapricorn,
    Piscis: mdiZodiacPisces,
    Leo: mdiZodiacLeo,
    Libra: mdiZodiacLibra,
    Gemini: mdiZodiacGemini,
    Sagitario: mdiZodiacSagittarius,
    Tauro: mdiZodiacTaurus,
    Virgo: mdiZodiacVirgo,
  };


  $: selectedIcon = icons[zodiacName];
  let dailyQuote = 'Evita tomar decisiones apresuradas en tus finanzas. Conflictos que evaluar con familiares para resolver problemas o malos entendidos.';
  let dateRange = '03-03 al 09-03-25';
  let igHandle = '@lucesastrales';

  let zodiacNameSize = 24;
  let dailyQuoteSize = 12;
  let dateRangeSize = 12;
  let igHandleSize = 24;

  function handleZodiacNameChange(event) {
    zodiacName = event.target.value;
  }
</script>
<div id="page-content">


  <div id="download-div" style="width: 360px; height: 360px; {backgroundImageSrc ? `background-image: url(${backgroundImageSrc});` : ''}/* Set your desired content here */" class="box">
  <svg width={iconSize} height={iconSize} viewBox="0 0 24 24" fill={iconColor}>
  <path d={selectedIcon} />
</svg>
<h1 class="zodiacName" style="font-size: {zodiacNameSize}px; color: {iconColor}">{zodiacName}</h1>
  <h3 style="font-size: {dailyQuoteSize}px; color: {iconColor}">{dailyQuote}</h3>
  <h4 style="font-size: {dateRangeSize}px; color: {iconColor}">{dateRange}</h4>
  <h2 style="font-size: {igHandleSize}px; color: {igColor}">{igHandle}</h2>
  </div>



<div class="containerInputs">
  <br />
<div>
  <label>
    Imagen de fondo:
<input type="file" accept="image/*" on:change={handleBackgroundImageChange} />
  </label>
</div>
  <br />
  <div>
    <label for="icon-color">Colores</label>
    <select id="icon-color" bind:value={iconColor}>
      {#each colors as color}
        <option value={color}>{color}</option>
      {/each}
    </select>
  </div>
  <br />

  <div>

    <label >Icono</label>
    <input type="range" id="icon-size" min="10" max="100" bind:value={iconSize} />
  </div>


<div>
  <label for="zodiac-select">Signo</label>
  <select id="zodiac-select" on:change={handleZodiacNameChange}>
    {#each Object.keys(icons) as iconName}
      <option value={iconName}>{iconName}</option>
    {/each}
  </select>
    <input type="range" id="zodiac-name-size" min="10" max="100" bind:value={zodiacNameSize} />
</div>
  <br />
<div>
  <label>
    Mensaje:
    <textarea bind:value={dailyQuote} />
    <input type="range" id="daily-quote-size" min="10" max="100" bind:value={dailyQuoteSize} />
  </label>
</div>

  <br />
  
<div>
  <label>
    Fecha:
    <input type="text" bind:value={dateRange} />
    <input type="range" id="date-range-size" min="10" max="100" bind:value={dateRangeSize} />
  </label>
</div>

  <br />
<div>
  <label>
     Instagram:
    <input type="text" bind:value={igHandle} />
    <input type="range" id="ig-handle-size" min="10" max="100" bind:value={igHandleSize} />
  </label>
<div>
    <label for="icon-color">IG Color:</label>
    <select id="icon-color" bind:value={igColor}>
      {#each colors as color}
        <option value={color}>{color}</option>
      {/each}
    </select>
  </div>

</div>
  <br />


<div>
  <label>
    Descargar Imagen:
<button on:click={downloadImage}>Download Image</button>
  </label>
</div>

</div>

</div>
<style>
  textarea {
    resize: vertical;
  }
  #page-content{
  	display: grid;
  	grid-template-columns: 1fr;
  	justify-items: center;
    background-color: #333;
  padding-block: 40px;

  }
  .containerInputs {
    color:white;
  	font-size: medium;
  }

  .zodiacName {
    text-transform: uppercase;
  }

  .box {
    text-align: center;
    /* Add more styles here for positioning and layout */
  display: block;
  overflow: hidden;
  background-size: cover; /* Ensure the image covers the entire div */
    background-position: center; /* Center the image */
  }
</style>
