<script lang="ts">
    import { onMount } from 'svelte';
    import { Chart } from 'chart.js/auto';
    
    const baseURL = "https://openehr-bootcamp.medblocks.com/ehrbase/rest/openehr/v1/query/aql"
    let data: {
        systolic: number,
        diastolic: number,
        timestamp: string,
        template_id: string
    }[] = []
    const getData = async (activeView: 'my-template' | 'all-readings') => {
        const response = await fetch(baseURL, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                q: `SELECT 
                bp/data[at0001]/events[at0006]/data[at0003]/items[at0004]/value/magnitude as systolic,
                bp/data[at0001]/events[at0006]/data[at0003]/items[at0005]/value/magnitude as diastolic, 
                c/context/start_time/value as timestamp,
                c/archetype_details/template_id/value as template_id  
                FROM EHR e CONTAINS COMPOSITION c 
                CONTAINS OBSERVATION bp [openEHR-EHR-OBSERVATION.blood_pressure.v2] 
                WHERE e/ehr_id/value = '6adc37f8-fff8-4fe4-a988-327b9fe6d5ac' 
                ${activeView === 'my-template' ? `AND c/archetype_details/template_id/value = 'nursing_vital_signs_sidharth.v0'` : ''}
                ORDER BY c/context/start_time/value
                `
            })
        })
        const responseData = await response.json()
        const rows = responseData.rows.map((row: any) => {
            return {
                systolic: row[0],
                diastolic: row[1],
                timestamp: row[2],
                template_id: row[3]
            }
        })
        data = rows
        return rows
    }
    let activeView: 'my-template' | 'all-readings' = 'my-template'
    
    let chartCanvas: HTMLCanvasElement;
    let chart: Chart;

    

    $: if (chartCanvas && data) {
        // Destroy existing chart if it exists
        if (chart) chart.destroy();
        
        // Create new chart
        chart = new Chart(chartCanvas, {
            type: 'line',
            data: {
                labels: data.map(row => new Date(row.timestamp).toLocaleString()),
                datasets: [
                    {
                        label: 'Systolic',
                        data: data.map(row => row.systolic),
                        borderColor: 'rgb(255, 99, 132)',
                        tension: 0.1
                    },
                    {
                        label: 'Diastolic',
                        data: data.map(row => row.diastolic),
                        borderColor: 'rgb(54, 162, 235)',
                        tension: 0.1
                    }
                ]
            },
            options: {
                responsive: true,
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: 'Blood Pressure (mmHg)'
                        }
                    },
                    x: {
                        title: {
                            display: true,
                            text: 'Time'
                        }
                    }
                },
                plugins: {
                    tooltip: {
                        callbacks: {
                            afterBody: (context) => {
                                const dataIndex = context[0].dataIndex;
                                return `Template: ${data[dataIndex].template_id}`;
                            }
                        }
                    }
                }
            }
        });
    }
</script>
<div class="p-10">
<div class="flex gap-2 my-4">
    <button 
        class={`px-4 py-2 rounded-md transition-colors ${
            activeView === 'my-template' 
            ? 'bg-blue-500 text-white' 
            : 'bg-gray-100 hover:bg-gray-200 text-gray-700'
        }`}
        on:click={() => activeView = 'my-template'}>
        My template
    </button>
    <button 
        class={`px-4 py-2 rounded-md transition-colors ${
            activeView === 'all-readings' 
            ? 'bg-blue-500 text-white' 
            : 'bg-gray-100 hover:bg-gray-200 text-gray-700'
        }`}
        on:click={() => activeView = 'all-readings'}>
        All readings
    </button>
</div>
{#await getData(activeView)}
    <p>Loading...</p>
{:then data} 
    <table class="w-full border-collapse">
        <thead>
            <tr class="bg-gray-100">
                <th class="border p-2 text-left">Template ID</th>
                <th class="border p-2 text-left">Timestamp</th>
                <th class="border p-2 text-left">Systolic</th>
                <th class="border p-2 text-left">Diastolic</th>
            </tr>
        </thead>
        <tbody>
            {#each data as row}
                <tr class="border-b hover:bg-gray-50">
                    <td class="border p-2">{row.template_id}</td>
                    <td class="border p-2">{row.timestamp}</td>
                    <td class="border p-2">{row.systolic}</td>
                    <td class="border p-2">{row.diastolic}</td>
                </tr>
            {/each}
        </tbody>
    </table>
    
    <div class="mt-8">
        <canvas bind:this={chartCanvas}></canvas>
    </div>
{/await}
</div>
