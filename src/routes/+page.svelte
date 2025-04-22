<!--
  This example requires updating your template:

  ```
  <html class="h-full bg-gray-50">
  <body class="h-full">
  ```
-->
<script lang="ts">
    import { goto } from "$app/navigation";
    import Transition from 'svelte-transition'
  
    let pwd = $state(``);
    let showToast = $state(false);
  
    const checkPwd = ( str: string ) => { 
      if ( str == import.meta.env.VITE_PWD ) { 
        goto(`/app/ask`) 
      } else {
        showToast = true;
      }
      };
  </script>
  
  <div class="flex min-h-full flex-col justify-center py-12 sm:px-6 lg:px-8">
      <div class="sm:mx-auto sm:w-full sm:max-w-md">
        <img class="mx-auto h-10 w-auto" src="/mistral-logo.png" alt="Your Company">
        <h2 class="mt-6 text-center text-2xl/9 font-bold tracking-tight text-gray-900">What are the rules of ... ?</h2>
      </div>
    
      <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-[480px]">
        <div class="bg-white px-6 py-12 shadow-sm sm:rounded-lg sm:px-12">          
            <div class="mb-6">
              <label for="password" class="block text-sm/6 font-medium text-gray-900">Password</label>
              <div class="mt-2">
                <input type="password" bind:value={pwd} name="password" id="password" autocomplete="current-password" required class="block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-[#FA500F] sm:text-sm/6">
              </div>
            </div>
    
            <div>
              <button  type="submit" onclick={()=>checkPwd(pwd)} class="flex w-full justify-center rounded-md bg-[#FA500F] px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-[#FF6E00] focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#FA500F]">Sign in</button>
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
                <svg class="size-6 text-[#FF0511]" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
                  <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                </svg>
              </div>
              <div class="ml-3 w-0 flex-1 pt-0.5">
                <p class="text-sm font-medium text-gray-900">Wrong password!</p>
                <p class="mt-1 text-sm text-gray-500">Try again with the password provided.</p>
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