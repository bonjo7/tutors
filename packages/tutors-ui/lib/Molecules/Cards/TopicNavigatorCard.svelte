<script lang="ts">
  import type { Topic } from "tutors-reader-lib/src/models/topic";
  import type { Lo } from "tutors-reader-lib/src/types/lo-types";
  import { Image, TopicNavigator } from "tutors-ui";
  import { currentLo, layout } from "tutors-reader-lib/src/stores/stores";
  import { onDestroy } from "svelte";

  export let topic: Topic;

  let imageHeight = "";
  let headingText = "";
  let text = "";
  let cardWidths = "";
  let lo: Lo;
  const unsubscribe = layout.subscribe((layout) => {
    if (layout === "compacted") {
      headingText = "text-xs font-semibold";
      cardWidths = "w-52";
    } else {
      headingText = "text-md font-semibold";
      cardWidths = "w-72";
    }
  });
  currentLo.subscribe((current) => {
    lo = current;
  });
  onDestroy(unsubscribe);
  // onDestroy(unsubscribeLo);
</script>

  <div class="card {cardWidths} px-4 py-2">
    <h3 class="px-4 py-2 text-center {headingText}">{topic?.lo?.title}</h3>
    <div class="card-body">
      <figure class="flex justify-center p-2">
        <Image lo="{lo}" />
      </figure>
      <TopicNavigator topic="{topic}" />
    </div>
  </div>
