<script>
  import { tick } from "svelte";
  import Tile from "./Tile.svelte";
  const parameters = {
    easy: { column: 9, row: 9, mines: 10 },
    medium: { column: 16, row: 16, mines: 40 },
    hard: { column: 32, row: 18, mines: 99 },
  };
  let difficulty = $state("easy"),
    totalColumns = $derived(parameters[difficulty].column),
    totalRows = $derived(parameters[difficulty].row),
    totalMines = $derived(parameters[difficulty].mines),
    markCount = $state(0),
    minesLeft = $derived(totalMines - markCount),
    openCount = $state(0),
    safesLeft = $derived(totalColumns * totalRows - totalMines - openCount),
    isGameOver = $state(false);
  const generateMineCoordsEx = () => {
    // alternative: ++ to adjacent tiles, count adjacent mine
    let tiles = Array.from(
        { length: totalRows * totalColumns },
        (_, idx) => idx
      ),
      m = tiles.length;
    // while (m) {
    for (let t = totalMines + 1; t > 0; t--) {
      let i = Math.floor(Math.random() * m--);
      [tiles[m], tiles[i]] = [tiles[i], tiles[m]];
    }
    let minesIndices = tiles.slice(-(totalMines + 1)),
      minesCoords = minesIndices.map(
        (val) => `${val % totalColumns},${Math.trunc(val / totalColumns)}`
      );
    return minesCoords;
  };
  let mineCoordsEx = $state(generateMineCoordsEx()),
    mineCoords = $derived(mineCoordsEx.slice(1));
  const resetGrid = () => {
    markCount = 0;
    openCount = 0;
    isGameOver = false;
    mineCoordsEx = generateMineCoordsEx();
  };
</script>

<div
  class="select-none p-3 w-fit max-h-full max-w-full bg-gray-400 border-4 border-[#7b7b7b] border-t-white border-l-white mx-auto"
  role="group"
  oncontextmenu={(e) => {
    e.preventDefault();
  }}
>
  <div
    class="h-12 bg-gray-200 flex justify-between items-center p-2 mb-3 border-4 border-[#7b7b7b] border-b-white border-r-white"
  >
    <select class="w-10" bind:value={difficulty} onchange={resetGrid}>
      <option value="easy">易</option>
      <option value="medium">中</option>
      <option value="hard">難</option>
    </select>
    <button class="border-4 border-white px-1" onclick={resetGrid}>
      {!isGameOver ? ":)" : !safesLeft ? ":D" : ":("}
    </button>
    <div class="w-10 text-right font-mono">
      {minesLeft.toString().padStart(2, "0")}
    </div>
  </div>
  <div
    class="grid border-4 border-[#7b7b7b] border-b-white border-r-white"
    style="grid-template-columns: repeat({totalColumns}, 1fr);"
  >
    {#key mineCoordsEx}
      {#each { length: totalRows } as _, iy (iy)}
        {#each { length: totalColumns } as _, ix (ix)}
          {@const id = `${ix},${iy}`}
          <Tile
            {id}
            {safesLeft}
            hasMine={mineCoords.includes(id)}
            bind:openCount
            bind:isGameOver
            onMark={(isMarked) => {
              markCount += !isMarked ? 1 : -1;
            }}
            replaceMine={() => {
              let index = mineCoordsEx.findIndex((val) => val === id);
              mineCoordsEx[index] = mineCoordsEx[0];
              tick().then(() => {
                document.getElementById(id)?.click();
              });
            }}
            countAdjacentMines={() => {
              let mineCount = 0;
              for (
                let i = Math.max(ix - 1, 0);
                i <= Math.min(ix + 1, totalColumns);
                i++
              ) {
                for (
                  let j = Math.max(iy - 1, 0);
                  j <= Math.min(iy + 1, totalRows);
                  j++
                ) {
                  if (i === ix && j === iy) {
                    continue;
                  }
                  if (mineCoords.includes(`${i},${j}`)) {
                    mineCount++;
                  }
                }
              }
              return mineCount;
            }}
            openAdjacentTiles={() => {
              for (
                let i = Math.max(ix - 1, 0);
                i <= Math.min(ix + 1, totalColumns);
                i++
              ) {
                for (
                  let j = Math.max(iy - 1, 0);
                  j <= Math.min(iy + 1, totalRows);
                  j++
                ) {
                  if (i === ix && j === iy) {
                    continue;
                  }
                  let tile = document.getElementById(`${i},${j}`);
                  if (tile?.localName === "button") {
                    tick().then(() => {
                      tile?.click();
                    });
                  }
                }
              }
            }}
          />
        {/each}
      {/each}
    {/key}
  </div>
</div>
