<script lang="ts">
    export let provisionalDiagnosisCount = 1;
    export let medicationOrderCount = 1;
    export let serviceRequestCount = 1;
</script>
<h2 class="text-xl font-semibold mb-4">Provisional Diagnosis</h2>
{#each Array(provisionalDiagnosisCount) as _, index}
<div class="my-2">
        <mb-input path={`gynaec_case_record_sidharth.v0/problem_diagnosis:${index}/problem_diagnosis_name`}></mb-input>
        <mb-context bind={{value: 'Working', code: 'at0017', terminology: 'local'}} path={`gynaec_case_record_sidharth.v0/problem_diagnosis:${index}/problem_diagnosis_qualifier/diagnostic_status`}></mb-context>
        <mb-context bind={{value: 'Current', code: "at0062", terminology: "local"}} path={`gynaec_case_record_sidharth.v0/problem_diagnosis:${index}/problem_diagnosis_qualifier/current_past`}></mb-context>
        <mb-context path={`gynaec_case_record_sidharth.v0/problem_diagnosis:${index}/language`}></mb-context>
        <mb-context path={`gynaec_case_record_sidharth.v0/problem_diagnosis:${index}/encoding`}></mb-context>
        <mb-context path={`gynaec_case_record_sidharth.v0/problem_diagnosis:${index}/subject`}></mb-context>
    </div>
{/each}
<button 
    class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
    on:click={() => provisionalDiagnosisCount++}
>
    Add more
</button>
{#if provisionalDiagnosisCount > 1}
    <button 
    class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
    on:click={() => provisionalDiagnosisCount--}
    >
    Remove
    </button>
{/if}
<h2 class="text-xl font-semibold mb-4 mt-8">Final Diagnosis</h2>
<mb-input path="gynaec_case_record_sidharth.v0/final_diagnosis/problem_diagnosis_name"></mb-input>
<mb-context bind={{value: 'Established', code: 'at0018', terminology: 'local'}} path="gynaec_case_record_sidharth.v0/final_diagnosis/problem_diagnosis_qualifier/diagnostic_status" label="Diagnostic status" terminology="local"></mb-context>
<mb-context bind={{value: 'Current', code: 'at0062', terminology: 'local'}} path="gynaec_case_record_sidharth.v0/final_diagnosis/problem_diagnosis_qualifier/current_past" label="Current/Past?" terminology="local"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/final_diagnosis/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/final_diagnosis/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/final_diagnosis/subject"></mb-context>

<h2 class="text-xl font-semibold mb-4 mt-8">Medication Order</h2>
<div class="grid grid-cols-4 gap-4 mb-2">
    <div>
        <h3 class="mb-2">Medication</h3>
    </div>
    <div>
        <h3 class="mb-2">Directions</h3>
    </div>
    <div>
        <h3 class="mb-2">Start Date/Time</h3>
    </div>
    <div>
        <h3 class="mb-2">End Date/Time</h3>
    </div>
</div>

{#each Array(medicationOrderCount) as _, index}
    <div class="grid grid-cols-4 gap-4 mb-2">
        <mb-input path={`gynaec_case_record_sidharth.v0/medication_order/order:${index}/medication_item`}></mb-input>
        <mb-input path={`gynaec_case_record_sidharth.v0/medication_order/order:${index}/overall_directions_description`}></mb-input>
        <mb-date path={`gynaec_case_record_sidharth.v0/medication_order/order:${index}/order_details/order_start_date_time`}></mb-date>
        <mb-date path={`gynaec_case_record_sidharth.v0/medication_order/order:${index}/order_details/order_stop_date_time`}></mb-date>
        <mb-context path={`gynaec_case_record_sidharth.v0/medication_order/order:${index}/timing`}></mb-context>
    </div>
{/each}
<button 
    class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
    on:click={() => medicationOrderCount++}
>
    Add more
</button>
{#if medicationOrderCount > 1}
    <button 
    class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
    on:click={() => medicationOrderCount--}
    >
    Remove
    </button>
{/if}
<mb-context path="gynaec_case_record_sidharth.v0/medication_order/narrative"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/medication_order/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/medication_order/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/medication_order/subject"></mb-context>

<h2 class="text-xl font-semibold mb-4 mt-8">Service Requests</h2>
<div class="grid grid-cols-3 gap-4 mb-2">
    <div>
        <h3 class="mb-2">Service Name</h3>
    </div>
    <div>
        <h3 class="mb-2">Description</h3>
    </div>
    <div>
        <h3 class="mb-2">Service Due</h3>
    </div>
</div>

{#each Array(serviceRequestCount) as _, index}
    <div class="grid grid-cols-3 gap-4 mb-2">
        <mb-input path={`gynaec_case_record_sidharth.v0/service_request/current_activity:${index}/service_name`}></mb-input>
        <mb-input path={`gynaec_case_record_sidharth.v0/service_request/current_activity:${index}/description`}></mb-input>
        <mb-date path={`gynaec_case_record_sidharth.v0/service_request/current_activity:${index}/service_due`}></mb-date>
        <mb-context path={`gynaec_case_record_sidharth.v0/service_request/current_activity:${index}/timing`}></mb-context>
    </div>
{/each}
<button 
    class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
    on:click={() => serviceRequestCount++}
>
    Add more
</button>
{#if serviceRequestCount > 1}
    <button 
    class="px-3 py-1 text-sm rounded border border-gray-300 hover:bg-gray-100 transition-colors"
    on:click={() => serviceRequestCount--}
    >
    Remove
    </button>
{/if}
<mb-context path="gynaec_case_record_sidharth.v0/service_request/narrative"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/service_request/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/service_request/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/service_request/subject"></mb-context>