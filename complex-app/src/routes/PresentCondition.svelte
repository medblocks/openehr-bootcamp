<script lang="ts">
    export let symptomCount = 1;

    async function handleSearch({searchString}: {searchString: string}) {
        return [
            {
                code: '1',
                value: `Symptom ${searchString} 1`,
                terminology: 'SNOMED-CT',
            },
            {
                code: '2',
                value: `Symptom ${searchString} 2`,
                terminology: 'SNOMED-CT',
            },
            {
                code: '3',
                value: `Symptom ${searchString} 3`,
                terminology: 'SNOMED-CT',
            },
        ]
    }
</script>

<mb-input textarea path="gynaec_case_record_sidharth.v0/story_history/present_condition:0"></mb-input>

<h2 class="text-xl font-semibold mb-4 mt-8">Signs and Symptoms</h2>
<div class="grid grid-cols-3 gap-4">
    <div>
        <h3 class="mb-2">Symptom/Sign</h3>
    </div>
    <div>
        <h3 class="mb-2">Episode Onset</h3>
    </div>
    <div>
        <h3 class="mb-2">Episode Duration</h3>
    </div>
</div>
{#each Array(symptomCount) as _, index}
<div class="grid grid-cols-3 gap-4 mb-2">
    <div>
        <mb-search handleSearch={handleSearch} path={`gynaec_case_record_sidharth.v0/story_history/symptom_sign:${index}/symptom_sign_name`}></mb-search>
    </div>
    <div>
        <mb-date path={`gynaec_case_record_sidharth.v0/story_history/symptom_sign:${index}/episode_onset`}></mb-date>
    </div>
    <div>
        <mb-duration day path={`gynaec_case_record_sidharth.v0/story_history/symptom_sign:${index}/episode_duration`}></mb-duration>
    </div>
</div>
{/each}
<div class="flex space-x-2 mt-2">
  <button 
    class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
    on:click={() => symptomCount++}
  >
    Add more
  </button>
  {#if symptomCount > 1}
    <button 
      class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
      on:click={() => symptomCount--}
    >
      Remove
    </button>
  {/if}
</div>
<mb-context path="gynaec_case_record_sidharth.v0/story_history/time"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/story_history/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/story_history/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/story_history/subject"></mb-context>