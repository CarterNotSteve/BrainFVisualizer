<script lang="ts">
  import Tape from './tape.svelte';
	let table = [0,0,0,0,0,0,0,0,0];
  let speed = 25;
	let program = "";
  let input= "";
  let inputneeded = false;
  let active = 0;
  let ins_ptr = 0;
  let brackstack = [];
  let output = "";
  let pisclosed=true;

  function inputprocedure() {
    inputneeded = false;
    console.log(input);
    table[active] = input.charCodeAt(0);
    input = "";
    setTimeout(handlechar,500-speed*10,program[ins_ptr]);
  }

  function handlechar(char:string) {
    console.dir(ins_ptr);
    if (ins_ptr > program.length) {return}
    if (pisclosed) {
      switch(char){
          case "+":
            table[active] += 1;
            if (table[active] > 127) {
              table[active] = 0;
            }
            break;
          case "-":
            table[active] -= 1;
            if (table[active] < 0) {
              table[active] = 127;
            }
            break;
          case ".":
            output = output + String.fromCharCode(table[active]);
            break;
          case "[":
            if (!table[active]) {
              pisclosed=false;
            } else {
              brackstack.push(ins_ptr);
            }
            break;
          case "]":
            if (table[active] != 0) {
              pisclosed=true;
              ins_ptr = brackstack.pop() - 1;
              console.log("Closed!");
            }
            break;
          case ">":
            active++;
            if (active >= table.length){
              table.push(0);
            }
            break;
          case "<":
            active--;
            if (active < 0) {
              table.unshift(0);
              table=table;
              console.log("unshifted!")
              active = 0;
            }
            break;
          case ",":
            inputneeded = true;
      }
    }
    ins_ptr++;
    if (inputneeded) {return}
    if (!pisclosed) {setTimeout(handlechar,0,program[ins_ptr])}
    if (pisclosed) {setTimeout(handlechar,500-speed*10,program[ins_ptr])}
  }


  // brainF program
  function runbf() {
    table = [0,0,0,0,0,0,0,0,0];
    ins_ptr = 0;
    output = "";
    active = 0;
    setTimeout(handlechar,500-speed*10,program[ins_ptr]);
  }


</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fira+Code">


<Tape table={table} active={active}></Tape>

<div class="btnrow">
  <p style="margin-top:-0.4vh;" class="label">{speed}</p>
  <input bind:value={speed} min=0 max=50 step=1 style="inline-block" type="range" class="speedin"/>
</div>
{#if inputneeded}
<span class="label">input:</span><input style="height:2vh;width:1vw;" maxlength=1 id="inputBox" bind:value={input} class="area"/>
<button class="runbtn" on:click={inputprocedure}>Send</button>
{/if}
<button class="runbtn" on:click={runbf}>Run</button>
<div class="area" contenteditable bind:textContent={program}></div>
<p class="label">Output:</p>
<div class="area" style="height:3vw; margin-top:0;">{output}</div>