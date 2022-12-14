<script lang="ts">
  import {
    Combobox,
    ComboboxInput,
    ComboboxButton,
    ComboboxLabel,
    ComboboxOptions,
    ComboboxOption,
  } from '$lib';

  function classNames(...classes: (string | false | null | undefined)[]) {
    return classes.filter(Boolean).join(' ');
  }

  let people = [
    'Wade Cooper',
    'Arlene Mccoy',
    'Devon Webb',
    'Tom Cook',
    'Tanya Fox',
    'Hellen Schmidt',
    'Caroline Schultz',
    'Mason Heaney',
    'Claudie Smitham',
    'Emil Schaefer',
  ];

  let active: string | undefined;
  if (active === undefined) {
    active = people[Math.floor(Math.random() * people.length)];
  }
  let active2: string | undefined;
  if (active2 === undefined) {
    active2 = people[Math.floor(Math.random() * people.length)];
  }
  $: query = '';
  $: filteredPeople = query
    ? people.filter((item) => !!item.match(new RegExp(query, 'gi')))
    : people;

  $: query2 = '';
  $: filteredPeople2 = query2
    ? people.filter((item) => !!item.match(new RegExp(query, 'gi')))
    : people;

  function handleInput(e: CustomEvent) {
    const target = e.currentTarget as HTMLInputElement;
    query = target.value || '';
  }
  function handleInput2(e: CustomEvent) {
    const target = e.currentTarget as HTMLInputElement;
    query2 = target.value || '';
  }
</script>

<div class="w-64">
  <p>
    <strong>Value1: </strong>{active}<br />
    <strong>Value2: </strong>{active2}<br />
  </p>
  <div class="space-y-1">
    <Combobox
      value={active}
      on:change={(event) => {
        console.log('value:', event.detail);
        active = event.detail;
      }}
    >
      <ComboboxLabel class="block text-sm font-medium leading-5 text-gray-700">
        Assigned to
      </ComboboxLabel>

      <div class="relative">
        <div
          class="relative w-full cursor-default overflow-hidden rounded-lg bg-white text-left shadow-md focus:outline-none focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-teal-300 sm:text-sm"
        >
          <ComboboxInput
            class="w-full border-none py-2 pl-3 pr-10 text-sm leading-5 text-gray-900 focus:ring-0"
            on:input={handleInput}
            displayValue={(value) => `${value}`}
          />
          <ComboboxButton class="absolute inset-y-0 right-0 flex items-center pr-2">
            <svg
              class="w-5 h-5 text-gray-400"
              viewBox="0 0 20 20"
              fill="none"
              stroke="currentColor"
            >
              <path
                d="M7 7l3-3 3 3m0 6l-3 3-3-3"
                stroke-width="1.5"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </ComboboxButton>
        </div>

        <div class="absolute w-full mt-1 bg-white rounded-md shadow-lg  z-10">
          <ComboboxOptions
            class="py-1 overflow-auto text-base leading-6 rounded-md shadow-xs max-h-60 focus:outline-none sm:text-sm sm:leading-5"
          >
            {#each filteredPeople as name (name)}
              <ComboboxOption
                value={name}
                class={({ active }) => {
                  return classNames(
                    'relative py-2 pl-3 cursor-default select-none pr-9 focus:outline-none',
                    active ? 'text-white bg-indigo-600' : 'text-gray-900'
                  );
                }}
                let:active
                let:selected
              >
                <span
                  class={classNames(
                    'block truncate',
                    selected ? 'font-semibold' : 'font-normal'
                  )}
                >
                  {name}
                </span>
                {#if selected}
                  <span
                    class={classNames(
                      'absolute inset-y-0 right-0 flex items-center pr-4',
                      active ? 'text-white' : 'text-indigo-600'
                    )}
                  >
                    <svg class="w-5 h-5" viewBox="0 0 20 20" fill="currentColor">
                      <path
                        fill-rule="evenodd"
                        d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                        clip-rule="evenodd"
                      />
                    </svg>
                  </span>
                {/if}
              </ComboboxOption>
            {/each}
          </ComboboxOptions>
        </div>
      </div>
    </Combobox>

    <Combobox
      value={active2}
      on:change={(event) => {
        console.log('value:', event.detail);
        active2 = event.detail;
      }}
    >
      <ComboboxLabel class="block text-sm font-medium leading-5 text-gray-700">
        Assigned to
      </ComboboxLabel>

      <div class="relative">
        <div
          class="relative w-full cursor-default overflow-hidden rounded-lg bg-white text-left shadow-md focus:outline-none focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-teal-300 sm:text-sm"
        >
          <ComboboxInput
            class="w-full border-none py-2 pl-3 pr-10 text-sm leading-5 text-gray-900 focus:ring-0"
            on:input={handleInput2}
            displayValue={(value) => `${value}`}
          />
          <ComboboxButton class="absolute inset-y-0 right-0 flex items-center pr-2">
            <svg
              class="w-5 h-5 text-gray-400"
              viewBox="0 0 20 20"
              fill="none"
              stroke="currentColor"
            >
              <path
                d="M7 7l3-3 3 3m0 6l-3 3-3-3"
                stroke-width="1.5"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </ComboboxButton>
        </div>

        <div class="absolute w-full mt-1 bg-white rounded-md shadow-lg  z-10">
          <ComboboxOptions
            class="py-1 overflow-auto text-base leading-6 rounded-md shadow-xs max-h-60 focus:outline-none sm:text-sm sm:leading-5"
          >
            {#each filteredPeople2 as name (name)}
              <ComboboxOption
                value={name}
                class={({ active }) => {
                  return classNames(
                    'relative py-2 pl-3 cursor-default select-none pr-9 focus:outline-none',
                    active ? 'text-white bg-indigo-600' : 'text-gray-900'
                  );
                }}
                let:active
                let:selected
              >
                <span
                  class={classNames(
                    'block truncate',
                    selected ? 'font-semibold' : 'font-normal'
                  )}
                >
                  {name}
                </span>
                {#if selected}
                  <span
                    class={classNames(
                      'absolute inset-y-0 right-0 flex items-center pr-4',
                      active ? 'text-white' : 'text-indigo-600'
                    )}
                  >
                    <svg class="w-5 h-5" viewBox="0 0 20 20" fill="currentColor">
                      <path
                        fill-rule="evenodd"
                        d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                        clip-rule="evenodd"
                      />
                    </svg>
                  </span>
                {/if}
              </ComboboxOption>
            {/each}
          </ComboboxOptions>
        </div>
      </div>
    </Combobox>
  </div>
</div>
