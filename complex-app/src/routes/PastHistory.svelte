<script lang="ts">
    export let familyMemberCount = 1;

    async function handleSearch({searchString}: {searchString: string}) {
        return [
            {
                code: '1',
                value: `Diabetes`,
                terminology: 'SNOMED-CT',
            },
            {
                code: '2',
                value: `Hypertension`,
                terminology: 'SNOMED-CT',
            },
            {
                code: '3',
                value: `Asthma`,
                terminology: 'SNOMED-CT',
            },
        ]
    }
</script>
<mb-search handleSearch={handleSearch} path="gynaec_case_record_sidharth.v0/past_history/problem_diagnosis_name"></mb-search>
<mb-context bind={{"value": "Past", "code": "at0061", "terminology": "local"}} path="gynaec_case_record_sidharth.v0/past_history/problem_diagnosis_qualifier/current_past"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/past_history/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/past_history/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/past_history/subject"></mb-context>

<h2 class="text-xl font-semibold mb-4 mt-8">Family History</h2>
<mb-input textarea path="gynaec_case_record_sidharth.v0/family_history/summary" label="Summary"></mb-input>
<div>
    <div class="grid grid-cols-2 gap-4 mt-2">
        <div>
            <h3 class="mb-2">Relationship</h3>
        </div>
        <div>
            <h3 class="mb-2">Problem/diagnosis name</h3>
        </div>
    </div>
    {#each Array(familyMemberCount) as _, index}
    <div class="grid grid-cols-2 gap-4 mb-2">
        <div>
            <mb-text-select path={`gynaec_case_record_sidharth.v0/family_history/per_family_member:${index}/relationship`}>
              <mb-option value="father" label="Father"></mb-option>
              <mb-option value="mother" label="Mother"></mb-option>
              <mb-option value="sibling" label="Sibling"></mb-option>
              <mb-option value="other" label="Other"></mb-option>
            </mb-text-select>
        </div>
        <div>
            <mb-search handleSearch={handleSearch} path={`gynaec_case_record_sidharth.v0/family_history/per_family_member:${index}/clinical_history:0/problem_diagnosis_name`}></mb-search>
        </div>
    </div>
    {/each}
    <div class="flex space-x-2 mt-2">
        <button 
          class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
          on:click={() => familyMemberCount++}
        >
          Add more
        </button>
        {#if familyMemberCount > 1}
          <button 
            class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
            on:click={() => familyMemberCount--}
          >
            Remove
          </button>
        {/if}
      </div>
</div>
<mb-context path="gynaec_case_record_sidharth.v0/family_history/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/family_history/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/family_history/subject"></mb-context>