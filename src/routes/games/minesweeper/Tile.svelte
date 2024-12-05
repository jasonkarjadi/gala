<script>
  let {
      id,
      safesLeft,
      hasMine,
      openCount = $bindable(0),
      isGameOver = $bindable(false),
      onMark,
      replaceMine,
      countAdjacentMines,
      openAdjacentTiles,
    } = $props(),
    isOpen = $state(false),
    isMarked = $state(false),
    icon = $derived(hasMine ? "💣" : countAdjacentMines());
  const numberColors = {
      1: "#0100fe",
      2: "#008001",
      3: "#fe0000",
      4: "#010080",
      5: "#810102",
      6: "#008081",
      7: "#000000",
      8: "#808080",
    },
    tileStyle =
      "size-7 content-center text-center bg-[#c0c0c0] border-[#7b7b7b]";
</script>

{#snippet openTile(isRedBg)}
  <div
    class="{tileStyle} border-t-2 border-l-2 font-bold font-mono leading-none text-xl"
    class:bg-red-600={isRedBg}
    class:text-2xl={!hasMine}
    style={!hasMine && icon !== 0 && `color: ${numberColors[icon]};`}
  >
    {#if icon !== 0}{icon}{/if}
  </div>
{/snippet}

{#if !isOpen}
  {#if isGameOver && safesLeft && hasMine && !isMarked}
    {@render openTile(false)}
  {:else}
    <button
      {id}
      class="{tileStyle} border-4 border-t-white border-l-white text-sm {isMarked &&
        'bg-[#a0a0a0]'}"
      onclick={(e) => {
        if (isGameOver || isOpen) return;
        if (isMarked) {
          if (e.isTrusted) return;
          onMark(isMarked);
        }
        if (hasMine) {
          if (!openCount) {
            replaceMine();
          } else {
            isOpen = true;
            isGameOver = true;
            return;
          }
        }
        openCount++;
        if (!safesLeft) {
          isGameOver = true;
        } else if (!icon) {
          openAdjacentTiles();
        }
        isOpen = true;
      }}
      oncontextmenu={(e) => {
        e.preventDefault();
        if (isGameOver) return;
        onMark(isMarked);
        isMarked = !isMarked;
      }}
    >
      {#if isMarked || (!safesLeft && hasMine)}🚩{/if}
    </button>
  {/if}
{:else}
  {@render openTile(hasMine)}
{/if}
