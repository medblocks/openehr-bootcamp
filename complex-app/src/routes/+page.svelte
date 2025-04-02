<script lang="ts">
    import "medblocks-ui";
    import "medblocks-ui/dist/styles";
    import PresentCondition from "./PresentCondition.svelte";

    let selectedComposition: any;

    import {count} from 'medblocks-ui/dist/utils'
    
    import PastHistory from "./PastHistory.svelte";
    import SexualHistory from "./SexualHistory.svelte";
    import Examination from "./Examination.svelte";
    import DiagnosisRecommendations from "./DiagnosisRecommendations.svelte";


    // let symptomCount = count(composition, 'gynaec_case_record_sidharth.v0/story_history/symptom_sign')

    let currentStep = 0;
    let form: any;
    let ehrId = 'f9e7debe-070a-438d-ad2d-bfbfcc7e0c4c'
    let templateId = 'gynaec_case_record_sidharth.v0'

    let symptomCount = 1;
    let familyMemberCount = 1;
    let medicationOrderCount = 1;
    let serviceRequestCount = 1;
    let provisionalDiagnosisCount = 1;
    const handleEdit = async (uid: string) => {
        const response = await fetch(`https://openehr-bootcamp.medblocks.com/ehrbase/rest/openehr/v1/ehr/${ehrId}/composition/${uid}`, {
            method: 'GET',
            headers: {
                'Accept': 'application/openehr.wt.flat.schema+json',
            }
        })
        const data = await response.json()
        selectedComposition = data
        symptomCount = count(data, 'gynaec_case_record_sidharth.v0/story_history/symptom_sign')
        familyMemberCount = count(data, 'gynaec_case_record_sidharth.v0/family_history/per_family_member')
        medicationOrderCount = count(data, 'gynaec_case_record_sidharth.v0/medication_order/order')
        serviceRequestCount = count(data, 'gynaec_case_record_sidharth.v0/service_request/current_activity')
        provisionalDiagnosisCount = count(data, 'gynaec_case_record_sidharth.v0/problem_diagnosis')
        form.import(data)
    }

    const listCompositions = async () => {
        const response = await fetch(`https://openehr-bootcamp.medblocks.com/ehrbase/rest/openehr/v1/query/aql`, {
            method: 'POST',
            body: JSON.stringify({
                "q": `SELECT c/context/start_time/value as time, c/uid/value as uid FROM EHR e CONTAINS COMPOSITION c WHERE e/ehr_id/value = '${ehrId}' AND c/archetype_details/template_id/value = '${templateId}' ORDER BY c/context/start_time/value`
            }),
            headers: {
                'Content-Type': 'application/json',
            }
        })
        const data = await response.json()
        // Convert the array data to an array of objects with time and uid properties
        const formattedData = data.rows.map((row: any) => ({
            time: row[0],
            uid: row[1]
        }));
        return formattedData;
    }
    const handleSubmit = async () => {
        const composition = form.export()
        console.log(composition);
        const response = await fetch(`https://openehr-bootcamp.medblocks.com/ehrbase/rest/openehr/v1/ehr/${ehrId}/composition?templateId=${templateId}`, {
            method: 'POST',
            headers: {
                'Accept': 'application/openehr.wt.flat.schema+json',
                'Content-Type': 'application/openehr.wt.flat.schema+json',
                'Prefer': 'return=representation',
            },
            body: JSON.stringify(composition),
        })
        const data = await response.json()
        console.log(data);
    }

    // onMount(()=>{
    //     form.import(composition)
    // })
</script>

<div class="w-full max-w-4xl mx-auto p-4">
  <div class="mb-4">
    <ul class="flex flex-wrap -mb-px text-sm font-medium text-center">
      {#each ['Present Condition', 'Past History', 'Sexual History', 'Examination', 'Diagnosis & Recommendations'] as section, index}
        <li class="mr-2">
          <button 
            class={`inline-block p-4 border-b-2 rounded-t-lg ${currentStep === index ? 'text-blue-600 border-blue-600' : 'border-transparent hover:text-gray-600 hover:border-gray-300'}`}
            on:click={() => currentStep = index}
          >
            {section}
          </button>
        </li>
      {/each}
    </ul>
  </div>
<mb-form bind:this={form}>
    <mb-context path="gynaec_case_record_sidharth.v0/category"></mb-context>
    <mb-context path="gynaec_case_record_sidharth.v0/language"></mb-context>
    <mb-context path="gynaec_case_record_sidharth.v0/territory"></mb-context>
    <mb-context path="gynaec_case_record_sidharth.v0/composer"></mb-context>
    <mb-context path="gynaec_case_record_sidharth.v0/context/setting"></mb-context>
    <mb-context path="gynaec_case_record_sidharth.v0/context/start_time"></mb-context>
  <div class="bg-white rounded-lg shadow-md p-6 mb-4">
    <div class:hidden={currentStep !== 0}>
      <h2 class="text-xl font-semibold mb-4">Present Condition</h2>
      <PresentCondition symptomCount={symptomCount} />
    </div>
    <div class:hidden={currentStep !== 1}>
      <h2 class="text-xl font-semibold mb-4">Past History</h2>
      <PastHistory familyMemberCount={familyMemberCount} />
    </div>
    <div class:hidden={currentStep !== 2}>
      <h2 class="text-xl font-semibold mb-4">Sexual History</h2>
      <SexualHistory />
    </div>
    <div class:hidden={currentStep !== 3}>
      <h2 class="text-xl font-semibold mb-4">Examination</h2>
      <Examination />
    </div>
    <div class:hidden={currentStep !== 4}>
      <DiagnosisRecommendations medicationOrderCount={medicationOrderCount} serviceRequestCount={serviceRequestCount} provisionalDiagnosisCount={provisionalDiagnosisCount}/>
      <!-- Recommendations form fields go here -->
    </div>
  </div>
</mb-form>
  <div class="flex justify-between">
    <button 
      class="px-4 py-2 bg-gray-200 text-gray-700 rounded-lg hover:bg-gray-300 disabled:opacity-50 disabled:cursor-not-allowed"
      disabled={currentStep === 0}
      on:click={() => currentStep--}
    >
      Previous
    </button>
    <div>
        {#if currentStep !== 4}
        <button 
        class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 disabled:opacity-50 disabled:cursor-not-allowed"
        disabled={currentStep === 4}
        on:click={() => currentStep++}
      >
        Next
      </button>
      {:else}
        <button 
        class="px-4 py-2 bg-green-600 text-white rounded-lg hover:bg-green-700"
        on:click={handleSubmit}
      >
        Submit
      </button>
      {/if}
    </div>
    
</div>
<h2 class="text-xl font-semibold mt-8 mb-4">Compositions</h2>
{#await listCompositions()}
  <div>Loading...</div>
{:then compositions}
  {#each compositions as composition}
    <div class="p-4 rounded-lg shadow-sm mb-2 hover:bg-gray-50">
      <div class="font-medium">{composition.time}</div>
      <div class="text-xs text-gray-500 mt-1">UID: {composition.uid}</div>
      <div class="flex mt-2">
        <button on:click={()=>handleEdit(composition.uid)} class="px-3 py-1 text-sm rounded cursor-pointer border border-blue-300 text-blue-600 hover:bg-blue-50 transition-colors mr-2">
          Edit
        </button>
        <button class="px-3 py-1 text-sm rounded cursor-pointer border border-red-300 text-red-600 hover:bg-red-50 transition-colors">
          Delete
        </button>
      </div>
    </div>
  {/each}
{/await}
</div>

