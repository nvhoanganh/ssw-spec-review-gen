<script>
  import { createEventDispatcher } from "svelte";
  import TextField from "./TextField.svelte";
  import EditableList from "./EditableList.svelte";
  import TaskList from "./TaskList.svelte";

  const dispatch = createEventDispatcher();

  const submit = () => dispatch("submit");
  const addNew = k => {
    value[k] = [...value[k], ""];
  };
  const addNewPbi = () => {
    value["tasks"] = [...value["tasks"], { name: "", est: 4, mvp: true }];
  };
  export let name;
  export let value = {
    project: "",
    productOwner: {},
    techLead: {},
    stateManager: {},
    ui_areas: [],
    has_more: false,
    has_more: true,
    outscope: [],
    tasks: [],
    avgRate: 1300,
    avgRateDiscounted: 1285
  };
</script>

<style>

</style>

<main>
  <form>
    <div class="flex flex-wrap -mx-3 mb-6">
      <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
        <TextField bind:value={name} label="Company Name" />
      </div>
      <div class="w-full md:w-2/3 px-3">
        <TextField
          bind:value={value.project}
          placeholder="Rate Calculator App"
          label="Project Name" />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.productOwner.name}
          label="Product Owner: Name" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.productOwner.title}
          placeholder="CTO"
          label="Title" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField bind:value={value.productOwner.mobile} label="Mobile" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField bind:value={value.productOwner.email} label="Email" />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.techLead.name}
          label="SSW Tech Lead: Name" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.techLead.title}
          placeholder="CTO"
          label="Title" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField bind:value={value.techLead.mobile} label="Mobile" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField bind:value={value.techLead.email} label="Email" />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.stateManager.name}
          label="SSW State Manager: Name" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.stateManager.title}
          placeholder="CTO"
          label="Title" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField bind:value={value.stateManager.mobile} label="Mobile" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField bind:value={value.stateManager.email} label="Email" />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.avgRate}
          isNumber
          label="Avg. Rate (Standard)" />
      </div>
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <TextField
          bind:value={value.avgRateDiscounted}
          isNumber
          label="Avg. Rate (Discounted)" />
      </div>
    </div>
    <!-- areas -->
    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full px-3 mb-6 md:mb-0">
        <EditableList bind:value={value.ui_areas} label="Major Features" />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-4">
      <div class="w-full px-3 mb-6 md:mb-0">
        <button
          on:click|preventDefault={() => addNew('ui_areas')}
          type="button"
          class="bg-blue-100 hover:bg-blue-500 text-blue-800 font-semibold
          hover:text-white py-2 px-4 border border-blue-500
          hover:border-transparent rounded">
          Add Feature
        </button>
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full px-3 mb-6 md:mb-0">
        <EditableList bind:value={value.outscope} label="Out of Scope" />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-4">
      <div class="w-full px-3 mb-6 md:mb-0">
        <button
          on:click|preventDefault={() => addNew('outscope')}
          type="button"
          class="bg-blue-100 hover:bg-blue-500 text-blue-800 font-semibold
          hover:text-white py-2 px-4 border border-blue-500
          hover:border-transparent rounded">
          Add Outscope
        </button>
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full px-3 mb-6 md:mb-0">
        <TaskList
          bind:value={value.tasks}
          label="PBI List"
          avgRate={value.avgRate || 0}
          discountedRate={value.avgRateDiscounted || 0} />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-4">
      <div class="w-full px-3 mb-6 md:mb-0">
        <button
          on:click|preventDefault={addNewPbi}
          type="button"
          class="bg-blue-100 hover:bg-blue-500 text-blue-800 font-semibold
          hover:text-white py-2 px-4 border border-blue-500
          hover:border-transparent rounded">
          Add Task
        </button>
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
        <label class="w-full block text-gray-500">
          <input
            class="mr-2 leading-tight"
            type="checkbox"
            bind:checked={value.has_more} />
          <span
            class="uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
            Flexible scoping ?
          </span>
        </label>
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-6 mt-8">
      <div class="mx-auto">
        <button
          on:click|preventDefault={submit}
          class="bg-transparent hover:bg-blue-500 text-red-700 font-semibold
          hover:text-white py-2 px-4 border border-red-500
          hover:border-transparent rounded">
          Download Document
        </button>
      </div>
    </div>
  </form>
</main>
