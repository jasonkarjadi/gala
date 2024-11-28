<script>
  import PhotoMini from "$lib/icons/PhotoMini.svelte";
</script>

{#snippet cartridge({ link, image = null, name, ruby = "" })}
  <a
    href="./games/{link}"
    class="inline-block bg-slate-200 text-center group rounded w-24"
    class:pointer-events-none={!image}
  >
    <div
      class="rounded-t h-16 bg-cover content-center group-hover:border group-hover:border-b-0 *:mx-auto"
      style="background-image: url({image});"
    >
      {#if !image}<PhotoMini />{/if}
    </div>
    <div
      class="bg-slate-300 group-hover:bg-slate-400 group-hover:border group-active:bg-slate-500 rounded-b h-8 content-center"
    >
      {#if ruby}
        <ruby>{name}<rt>{ruby}</rt></ruby>
      {:else}
        <span>{name}</span>
      {/if}
    </div>
  </a>
{/snippet}

<div class="p-4 flex flex-wrap gap-4">
  {@render cartridge({
    link: "minesweeper",
    name: "掃海艇",
    ruby: "マインスイーパ",
    image: "/thumbnails/minesweeper.png",
  })}
  {@render cartridge({
    link: "blockbreaker",
    name: "煉瓦崩",
    ruby: "ブロックくずし",
  })}
  {@render cartridge({
    link: "battleship",
    name: "戦艦",
    ruby: "バトルシップ",
  })}
  {@render cartridge({
    link: "texasholdem",
    name: "ポーカー",
  })}
  <!-- {@render cartridge({
    link: "mahjong",
    name: "麻雀",
    ruby: "まーじゃん",
  })} -->
  {@render cartridge({
    link: "sugoroku",
    name: "双六",
    ruby: "すごろく",
  })}
  <!-- {@render cartridge({
    link: "shougi",
    name: "将棋",
    ruby: "しょうぎ",
  })}
  {@render cartridge({
    link: "chess",
    name: "西洋将棋",
    ruby: "チェス",
  })}
  {@render cartridge({
    link: "xiangqi",
    name: "象棋",
    ruby: "シャンチー",
  })} -->
  {@render cartridge({
    link: "bullethell",
    name: "弾幕",
    ruby: "バレットヘル",
  })}
  {@render cartridge({
    link: "bulletheaven",
    name: "逆弾幕",
    ruby: "バレットヘブン",
  })}
  {@render cartridge({
    link: "snake",
    name: "蛇",
    ruby: "スネーク",
  })}
  {@render cartridge({
    link: "towerdefense",
    name: "塔楼防衛",
    ruby: "タワーディフェンス",
  })}
  {@render cartridge({
    link: "rhythm",
    name: "律",
    ruby: "リズム",
  })}
  {@render cartridge({
    link: "tetris",
    name: "テトリス",
  })}
  {@render cartridge({
    link: "puyopuyo",
    name: "ぷよぷよ",
  })}
  {@render cartridge({
    link: "parkour",
    name: "パルクール",
  })}
  {@render cartridge({
    link: "math",
    name: "数学",
  })}
  <!-- {@render cartridge({
    link: "pinball",
    name: "ピンボール",
  })} -->
</div>
