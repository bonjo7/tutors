<script lang="ts">
  import Icon from "../../Atoms/Icon/Icon.svelte";
  import { getIcon } from "../../Atoms/Icon/themes";
  import type { Lo } from "tutors-reader-lib/src/types/lo-types";
  import { currentCourse, layout } from "tutors-reader-lib/src/stores/stores";
  import { onDestroy } from "svelte";
  import { Image } from "tutors-ui";
  import { convertMd } from "tutors-reader-lib/src/utils/markdown-utils";
  import { cardTransition } from "../../animations";

  export let lo: Lo;
  let target = "";
  if (lo.type === "web") {
    if (lo.route.startsWith("http")) {
      target = "_blank";
    }
  }

  if (lo) {
    if (lo.type == "video") {
      lo.route = lo.video;
    }
    lo.summary = convertMd(lo.summary, "");
  }

  let headingText = "";
  let cardWidths = "";

  const unsubscribe = layout.subscribe((layout) => {
    if (layout === "compacted") {
      headingText = "!text-md font-medium";
      cardWidths = "w-36 h-[18rem]";
    } else {
      headingText = "!text-lg font-semibold";
      cardWidths = "w-60 h-[24rem]";
    }
  });

  onDestroy(unsubscribe);
</script>

<a href="{lo.route}" target="{target}">
  <div transition:cardTransition class="card !bg-surface-50 dark:!bg-surface-700 border-y-8 border-{getIcon(lo.type).colour}-500 m-2 {cardWidths} transition-all hover:scale-105">
    <header class="card-header flex flex-row items-center justify-between p-3">
      <div class="inline-flex w-full">
        <div class="line-clamp-2 flex-auto {headingText} !text-black dark:!text-white">{lo.title}</div>
        {#if $currentCourse && !$currentCourse.areVideosHidden()}
          {#if lo.video && lo.type !== "video"}
            <a href="{lo.video}">
              <Icon type="video" />
            </a>
          {/if}
        {/if}
        <div class="flex-none"><Icon type="{lo.type}" /></div>
      </div>
    </header>
    <div class="card-body">
      <figure class="flex justify-center object-scale-down p-1">
        <Image lo="{lo}" />
      </figure>
    </div>
    <footer class="card-footer">
      <div class="prose dark:prose-invert line-clamp-3 text-center leading-6">
        {@html lo.summary}
      </div>
    </footer>
  </div>
</a>
