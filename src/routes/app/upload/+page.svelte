<script>
    import Transition from 'svelte-transition'

    let loading = $state(false);
    let data = $state('');
    let showToast = $state(false);

    const uploadData = async () => {
    console.log(`Data:`, data);
    loading = true;
    const result = await fetch(`https://mistral-be.thebeachhut.dev/files/text`, {
      method: `POST`,
      mode: 'cors',
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({"text": data})
    });
    const res = await result.json();
    data = '';
    let showToast = $state(false);

    console.log(res);
    loading = false;
  };
</script>

<div class="flex min-h-full flex-col justify-center py-12 sm:px-6 lg:px-8">
  <div class="sm:mx-auto sm:w-full sm:max-w-md">
    <img class="mx-auto h-10 w-auto" src="/mistral-logo.png" alt="Your Company">
    <div class="flex justify-center space-x-4 m-auto">
      <h2 class="mt-6 text-center text-2xl/9 font-bold tracking-tight text-gray-900">I want to </h2>
      <a href="/app/ask" class="mt-6 text-center text-2xl/9 font-bold tracking-tight text-gray-300 cursor-pointer">ask a question </a>
      <a href="/app/upload" class="mt-6 text-center text-2xl/9 font-bold tracking-tight underline text-[#FA500F]">load text </a>
    </div>    
  </div>
  <div class="mt-10 divide-y divide-gray-200 overflow-hidden rounded-lg bg-white shadow-sm">
    <div class="px-4 py-5 sm:p-6">
      <!-- Content goes here -->
      <div class="flex space-x-4">
        <img class="inline-block w-10 h-10 " src="/robot.png" alt="">
        <p class="place-self-center italic">"I'd love to learn new things"</p>
      </div>
    </div>
    <div class="px-4 py-5 sm:px-6">
        <div class="flex flex-col justify-between space-y-4">
          <textarea rows="10" bind:value={data} name="comment" id="comment" class="block w-full resize-none bg-transparent px-3 py-1.5 border rounded-lg border-gray-300 text-base text-gray-900 placeholder:text-gray-400 focus:outline-none sm:text-sm/6" placeholder="Type or copy/paste new data as text here... If you need to upload a pdf use the UI POC instead."></textarea>

            <button  type="submit" onclick={()=>uploadData()} class="flex w-full justify-center rounded-md bg-[#FA500F] px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-[#FF6E00] focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#FA500F]">
              {#if loading }
                <svg class=" animate-spin w-auto opacity-80" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><path d="M21 12a9 9 0 1 1-6.219-8.56"/></svg>
              {:else}
                Add text above to knowledge base
              {/if}
            </button>
        </div>      
    </div>

  </div>
</div>

<div aria-live="assertive" class="pointer-events-none fixed inset-0 flex items-end px-4 py-6 sm:items-start sm:p-6">
  <div class="flex w-full flex-col items-center space-y-4 sm:items-end">
    <Transition
      show={showToast}
      enter="transform ease-out duration-300 transition"
      enterFrom="translate-y-2 opacity-0 sm:translate-y-0 sm:translate-x-2"
      enterTo="translate-y-0 opacity-100 sm:translate-x-0"
      leave="transition ease-in duration-100"
      leaveFrom="opacity-100"
      leaveTo="opacity-0"
    >
      <div class="pointer-events-auto w-full max-w-sm overflow-hidden rounded-lg bg-white shadow-lg ring-1 ring-black/5">
        <div class="p-4">
          <div class="flex items-start">
            <div class="shrink-0">
              <svg class="size-6 text-green-400" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
                <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75 11.25 15 15 9.75M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
              </svg>
            </div>
            <div class="ml-3 w-0 flex-1 pt-0.5">
              <p class="text-sm font-medium text-gray-900">New rules uploaded!</p>
              <p class="mt-1 text-sm text-gray-500">You can now ask about this new game.</p>
            </div>
            <div class="ml-4 flex shrink-0">
              <button type="button" onclick={()=>showToast=false} class="inline-flex rounded-md bg-white text-gray-400 hover:text-gray-500 focus:ring-2 focus:ring-[#FA500F] focus:ring-offset-2 focus:outline-hidden">
                <span class="sr-only">Close</span>
                <svg class="size-5" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" data-slot="icon">
                  <path d="M6.28 5.22a.75.75 0 0 0-1.06 1.06L8.94 10l-3.72 3.72a.75.75 0 1 0 1.06 1.06L10 11.06l3.72 3.72a.75.75 0 1 0 1.06-1.06L11.06 10l3.72-3.72a.75.75 0 0 0-1.06-1.06L10 8.94 6.28 5.22Z" />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </div>
</div>
