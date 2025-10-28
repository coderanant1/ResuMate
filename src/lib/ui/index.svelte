<script lang="ts">
  import Editor from "../editor/index.svelte";
  import { ui } from "$lib/state/index.svelte";
  import { Tab, Tabs, TabsContent, TabsList } from "@haze-ui/svelte";

  let { children } = $props();

</script>

{#if ui.mode == "split"}
  <div class={`grid grid-cols-1 lg:grid-cols-2`}>
    <div class="sticky top-0 overflow-y-auto h-screen p-5 scrollbar">
      <Editor />
    </div>

    <div
      class="h-screen overflow-auto pt-5 flex justify-center items-start scrollbar"
    >
      <div
        class='doc'
        id="resume"
        style={`scale: ${Math.min(ui.viewScale, 100)}%`}
      >
        {@render children?.()}
      </div>
    </div>
  </div>
{:else}
  <div class={`grid gap-3 justify-center py-10 px-4`}>
    <Tabs>
      <TabsList class="mx-auto !bg-bg bg-muted tabon-(!bg-secondary)">
        <Tab value="editor"><i class="i-fa-regular:edit"></i>
          <span class="hidden sm:inline">Editor</span></Tab>
        <Tab value="viewer">
          <i class="i-fluent:eye-28-regular"></i> <span class="hidden sm:inline">Viewer</span></Tab>
      </TabsList>

      <TabsContent value="editor" class="max-w-[1000px]">
        <Editor />
      </TabsContent>

      <TabsContent
        value="viewer"
        class='doc'
        style={`scale: ${Math.min(ui.viewScale, 100)}%`}
        id="resume"
      >
        {@render children?.()}
      </TabsContent>
    </Tabs>
  </div>
{/if}
