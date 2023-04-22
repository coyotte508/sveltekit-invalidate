<script lang="ts">
  import { invalidate } from "$app/navigation";
  import { onMount } from "svelte";
  import type { LayoutData } from "./$types";

  export let data: LayoutData;

  onMount(() => {
    // Update exchange rates every 5 minutes
    const interval = setInterval(() => {
      console.log("invalidating");
      invalidate("/")
      invalidate((url) => {
        console.log("testing", url.href);
        return true;
      }).then(() => console.log("done"));
    }, 1000);

    return () => {
      clearInterval(interval);
      console.log("destroyed");
    };
  });
</script>

<slot />

{data.exchangeRate}