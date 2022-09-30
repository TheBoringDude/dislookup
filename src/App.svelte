<script lang="ts">
  import Card from "./components/Card.svelte";
  import type { LookupAPIResponse } from "./typings/response";

  let id = "";
  let fetching = false;
  let error = false;
  let data: LookupAPIResponse | undefined = undefined;

  const lookupId = async () => {
    if (id == "") return;

    fetching = true;

    const f = await fetch(`${import.meta.env.VITE_API}/id/${id}`);

    fetching = false;

    if (!f.ok) {
      error = true;
      return;
    }

    error = false;
    data = await f.json();
  };
</script>

<main class="w-5/6 mx-auto text-center">
  <div class="py-24">
    <header class="">
      <h1 class="text-3xl font-black">
        <span class="text-indigo-500">Discord</span> ID Lookup
      </h1>
    </header>

    <div class="mt-8">
      <div class="flex items-end justify-center">
        <div class="flex flex-col text-left">
          <label for="id" class="text-sm mb-1 text-gray-700"
            >Enter Discord id:</label
          >
          <input
            bind:value={id}
            id="id"
            name="id"
            class="border py-2 px-4 rounded-lg w-72 sm:w-96 text-sm"
            placeholder="Enter Discord id..."
          />
        </div>

        <button
          on:click={lookupId}
          disabled={fetching}
          class="border border-indigo-300 py-2 px-8 rounded-lg text-sm bg-indigo-400 hover:bg-indigo-500 text-white ml-2"
        >
          {#if fetching}
            lookup...
          {:else}
            lookup
          {/if}
        </button>
      </div>

      <hr class="my-6" />

      <div>
        {#if error}
          <p class="text-sm tracking-wide">Cannot find discord id...</p>
        {:else}
          <Card {data} />
        {/if}
      </div>
    </div>
  </div>
</main>
