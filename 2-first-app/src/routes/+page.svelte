<script lang="ts">
    import "medblocks-ui";
    import "medblocks-ui/dist/styles.js";
    import { Toaster, toast } from 'svelte-sonner'
    import webtemplate from './nursing_vital_signs_sidharth.v0.json'
    let ehrId = "6adc37f8-fff8-4fe4-a988-327b9fe6d5ac"
    let openEhrRestEndpoint = "https://openehr-bootcamp.medblocks.com/ehrbase/rest/openehr/v1"
    let form: any

    let updatingVitals: string | null = null

    async function submitVitals() {
        const composition = form.export()
        console.log(composition)
        const toastId = toast.loading('Loading...')
        if (!updatingVitals) {
            let response = await fetch(`${openEhrRestEndpoint}/ehr/${ehrId}/composition?templateId=${webtemplate.templateId}`, {
                method: "POST",
                body: JSON.stringify(composition),
                headers: {
                    "Content-Type": "application/openehr.wt.flat.schema+json",
                    "Accept": "application/openehr.wt.flat.schema+json",
                    "Prefer": "return=representation"
                }
            })
            let data = await response.json()
            console.log("Successfully created vitals", data)
        } else {
            const compositionId = updatingVitals.split("::")[0]
            let response = await fetch(`${openEhrRestEndpoint}/ehr/${ehrId}/composition/${compositionId}?templateId=${webtemplate.templateId}`, {
                method: "PUT",
                body: JSON.stringify(composition),
                headers: {
                    "Content-Type": "application/openehr.wt.flat.schema+json",
                    "Accept": "application/openehr.wt.flat.schema+json",
                    "Prefer": "return=representation",
                    "If-Match": updatingVitals
                }
            })
            let data = await response.json()
            console.log("Successfully updated vitals", data)
        }
        
        currentVitals = getVitals()
        toast.dismiss(toastId)
        toast.success("Vitals submitted successfully")
        form.import({})
    }

    async function getVitals() {
        let response = await fetch(`${openEhrRestEndpoint}/query/aql`, {
            method: "POST",
            body: JSON.stringify({
                "q": `SELECT c/uid/value, c/context/start_time/value from EHR e CONTAINS COMPOSITION c WHERE e/ehr_id/value='${ehrId}'`
                }),
            headers: {
                "Content-Type": "application/json"
            }
        })
        let data = await response.json()
        const rows = data.rows
        const vitals = rows.map((row: any) => {
            const [uid, timestamp] = row
            return { uid, timestamp }
        })
        return vitals
    }

    async function deleteVitals(uid: string) {
        let response = await fetch(`${openEhrRestEndpoint}/ehr/${ehrId}/composition/${uid}`, {
            method: "DELETE",
            headers: {
                "Content-Type": "application/json"
            }
        })
        console.log(response.status)
        toast.success("Vitals deleted successfully")
        currentVitals = getVitals()
    }

    async function importVitals(uid: string) {
        const toastId = toast.loading('Loading...')
        let response = await fetch(`${openEhrRestEndpoint}/ehr/${ehrId}/composition/${uid}`, {
            headers: {
                "Accept": "application/openehr.wt.flat.schema+json",
            }
        })
        let data = await response.json()
        form.import(data)
        updatingVitals = uid
        toast.dismiss(toastId)
    }

    let currentVitals = getVitals()

</script>
<Toaster />
<div class="flex w-full">
    <div class="w-1/2 p-4">
        <h2 class="text-xl font-semibold mb-4">{updatingVitals ? 'Updating Nursing Form' : 'Nursing Form'}</h2>
        
        <mb-auto-form bind:this={form} webTemplate={webtemplate}></mb-auto-form>
        <button on:click={submitVitals} class="mt-4 px-4 py-2 bg-gray-500 text-white rounded hover:bg-gray-600 float-right">
            Submit Vitals
        </button>
        {#if updatingVitals}
            <button on:click={()=>{updatingVitals = null; form.import({})}} class="mt-4 mr-2 px-4 py-2 bg-gray-500 text-white rounded hover:bg-gray-600 float-right">
                Cancel
            </button>
        {/if}
    </div>
    <div class="w-1/2 p-4 bg-gray-100">
        <h2 class="text-xl font-semibold mb-4">Previous Entries</h2>
        {#await currentVitals}
            <p>Loading...</p>
        {:then vitals}
            {#each vitals as vital}
                <div class="p-4 mb-4 bg-white rounded-lg shadow">
                    <div class="flex justify-between items-start">
                        <div>
                            <p class="text-gray-600 text-sm">{new Date(vital.timestamp).toLocaleDateString()}</p>
                            <p class="text-gray-400 text-xs mt-1">{new Date(vital.timestamp).toLocaleTimeString()}</p>
                            <p class="text-gray-500 text-xs mt-1">ID: {vital.uid}</p>
                        </div>
                        <div class="flex gap-2">
                            <button on:click={()=>importVitals(vital.uid)} class="px-3 py-1 text-sm text-blue-600 hover:bg-blue-50 rounded-md transition-colors duration-200">
                                Edit
                            </button>
                            <button on:click={()=>deleteVitals(vital.uid)} class="px-3 py-1 text-sm text-red-600 hover:bg-red-50 rounded-md transition-colors duration-200">
                                Delete
                            </button>
                        </div>
                    </div>
                </div>
            {/each}
        {/await}
    </div>
</div>