<script lang="ts">
  import type { LookupAPIResponse } from "src/typings/response";

  export let data: LookupAPIResponse | undefined;

  const getAvatar = (avatar: string | null) => {
    if (avatar == null) {
      return `https://cdn.discordapp.com/embed/avatars/${
        Number(data.discriminator) % 5
      }.png`;
    }

    return `https://cdn.discordapp.com/avatars/${data.id}/${avatar}.png?size=1024`;
  };
</script>

{#if data}
  <div
    class="shadow-2xl border border-gray-100 w-full sm:w-4/5 md:w-3/4 lg:w-2/3 xl:w-1/2 2xl:w-2/5 mx-auto rounded-lg flex flex-col md:flex-row items-center justify-center p-6"
  >
    <img
      class="h-40 w-40 rounded-lg object-contain"
      src={getAvatar(data.avatar)}
      alt={data.username}
    />

    <div class="md:ml-12 mt-4 md:mt-0 text-left text-lg">
      <p class="text-gray-500 my-0.5">
        ID: <span class="text-gray-700 font-bold">{data.id}</span>
      </p>

      <p class="text-gray-500 my-0.5">
        Username: <span class="text-gray-700 font-bold"
          >{data.username}#{data.discriminator}</span
        >
      </p>
    </div>
  </div>
{/if}
