<script>
  let question = $state('');
  let response = $state('');
  let loading = $state(false);
  const getAnswer = async () => {
    console.log(`Question:`, question);
    loading = true;
    const result = await fetch(`https://mistral-be/chat/question`, {
      method: `POST`,
      mode: 'cors',
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({"question": question})
    });
    const data = await result.json();
    console.log(data);
    response = data.result;
    loading = false;
  };
</script>

<div class="flex min-h-full flex-col justify-center py-12 sm:px-6 lg:px-8">
  <div class="sm:mx-auto sm:w-full sm:max-w-md">
    <img class="mx-auto h-10 w-auto" src="/mistral-logo.png" alt="Your Company">
    <div class="flex justify-center space-x-4 m-auto">
      <h2 class="mt-6 text-center text-2xl/9 font-bold tracking-tight text-gray-900">I Want to </h2>
      <a href="/app/ask" class="mt-6 text-center text-2xl/9 font-bold tracking-tight underline text-[#FA500F] cursor-pointer">ask a question </a>
      <a href="/app/upload" class="mt-6 text-center text-2xl/9 font-bold tracking-tight text-gray-300">load text </a>
    </div>    
  </div>
  <div class="mt-10 divide-y divide-gray-200 overflow-hidden rounded-lg bg-white shadow-sm">
    <div class="px-4 py-5 sm:px-6">
        <div class="flex justify-between space-x-4">
            <input type="text" bind:value={question} name="question" id="question" class="block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-[#FA500F] sm:text-sm/6" placeholder="Ask your question here.">
            <button  type="submit" onclick={()=>getAnswer()} class="flex w-24 justify-center rounded-md bg-[#FA500F] px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-[#FF6E00] focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#FA500F]">
              {#if loading }
                <svg class=" animate-spin w-auto opacity-80" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><path d="M21 12a9 9 0 1 1-6.219-8.56"/></svg>
              {:else}
                Ask
              {/if}
            </button>
        </div>      
    </div>
    <div class="px-4 py-5 sm:p-6">
      <!-- Content goes here -->
      <div class="flex items-start space-x-4">
        <div class="shrink-0">
          <img class="inline-block w-10 h-10 " src="/robot.png" alt="">
        </div>
        <div class="min-w-0 flex-1">
          <form action="#" class="relative">
            <div class="rounded-lg bg-white outline-1 border-0 -outline-offset-1 outline-gray-300 focus-within:outline-2 focus-within:-outline-offset-2 focus-within:outline-indigo-600">
              <label for="comment" class="sr-only"></label>
              <textarea rows="10" readonly bind:value={response} name="comment" id="comment" class="block w-full resize-none bg-transparent px-3 py-1.5 border-0 text-base text-gray-900 placeholder:text-gray-400 focus:outline-none sm:text-sm/6" placeholder="The answer will load here once received..."></textarea>
            </div>
          </form>
        </div>
      </div>
      
    </div>
  </div>
</div>
