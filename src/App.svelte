<script>
  import pangu from "pangu";
  import copy from "copy-to-clipboard";
  import { fly } from "svelte/transition";

  let text = "";
  $: panguText = pangu.spacing(text);

  function handlePanguClick() {
    if (panguText) {
      showMessage = true;
      copy(panguText);
      setTimeout(() => {
        showMessage = false;
      }, 1000);
    }
  }

  function init(el) {
    el.focus();
  }

  let showMessage = false;
</script>

<main class="flex h-screen">
  <div class="flex-1 flex flex-col p-6 bg-green-200">
    <h1 class="text-lg font-bold mb-2">输入</h1>
    <textarea
      use:init
      bind:value={text}
      class="w-full flex-1 placeholder:italic"
      placeholder="输入点什么..."
    />
  </div>
  <div class="flex-1 flex flex-col p-6 bg-purple-200">
    <h1 class="text-lg font-bold mb-2 flex justify-between">
      输出
      <span class="text-xs rounded-md text-gray-700 pr-3">
        Info 点击输出面板即可复制到剪切板</span
      >
    </h1>
    <textarea
      bind:value={panguText}
      on:click={handlePanguClick}
      class="w-full flex-1 placeholder:italic read-only:bg-slate-100"
      readonly
      placeholder="请在左侧输入..."
    />
  </div>
</main>
{#if showMessage}
  <div class="fixed inset-x-0 bottom-20 text-center" transition:fly>
    <span class="bg-green-200 mx-auto p-3 rounded-md border-green-600 border-2"
      >已经复制啦</span
    >
  </div>
{/if}
