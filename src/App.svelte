<script>
  import sample from './sample.js';

	let input = sample;
	let result = '';

	function numbering() {
    let countHeading1 = 0;
    let countHeading2 = 0;
    let countHeading3 = 0;
    let countHeading4 = 0;
    let countHeading5 = 0;
  
    result = input.replaceAll(/# (.*)\. /g, '# ').split('\n').map((line) => {
      if (line.startsWith('# ')) {
        countHeading2 = 0;
        return `${line.substring(0, 1)} ${++countHeading1}. ${line.substring(2)}`;
      } else if (line.startsWith('## ')) {
        countHeading3 = 0;
        return `${line.substring(0, 2)} ${countHeading1}-${++countHeading2}. ${line.substring(3)}`;
      } else if (line.startsWith('### ')) {
        countHeading4 = 0;
        return `${line.substring(0, 3)} ${countHeading1}-${countHeading2}-${++countHeading3}. ${line.substring(4)}`;
      } else if (line.startsWith('#### ')) {
        countHeading5 = 0
        return `${line.substring(0, 4)} ${countHeading1}-${countHeading2}-${countHeading3}-${++countHeading4}. ${line.substring(5)}`;
      } else if (line.startsWith('##### ')) {
        return `${line.substring(0, 5)} ${countHeading1}-${countHeading2}-${countHeading3}-${countHeading4}-${++countHeading5}. ${line.substring(6)}`;
      } else {
        return line;
      }
    }).join('\n');

		console.log(result);
	}
	numbering();
</script>

<main class="grid">
	<textarea on:keyup={numbering} on:blur={numbering} bind:value={input}></textarea>
	<textarea class="result">{result}</textarea>
</main>

<style>
	main {
		width: 100vw;
		height: 100vh;
	}

	main.grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
	}
	textarea {
		display: block;
		padding: 8px;
	}

	textarea.result {
		background-color: #eeeeee;
	}
</style>