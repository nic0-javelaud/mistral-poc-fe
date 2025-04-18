<script>
    let loading = $state(false);
    let data = $state('');

    const uploadData = async () => {
    console.log(`Data:`, data);
    loading = true;
    const result = await fetch(`https://mistral-be:8000/files/text`, {
      method: `POST`,
      mode: 'cors',
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({"text": data})
    });
    const res = await result.json();
    console.log(res);
    loading = false;
  };
</script>

<div class="flex min-h-full flex-col justify-center py-12 sm:px-6 lg:px-8">
  <div class="sm:mx-auto sm:w-full sm:max-w-md">
    <img class="mx-auto h-10 w-auto" src="/mistral-logo.png" alt="Your Company">
    <div class="flex justify-center space-x-4 m-auto">
      <h2 class="mt-6 text-center text-2xl/9 font-bold tracking-tight text-gray-900">I Want to </h2>
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
