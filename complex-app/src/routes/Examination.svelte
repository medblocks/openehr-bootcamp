<div class="flex flex-col gap-4">
    <mb-input textarea path="gynaec_case_record_sidharth.v0/physical_examination_findings/general/clinical_description" label="General examination"></mb-input>
    <mb-input textarea path="gynaec_case_record_sidharth.v0/physical_examination_findings/abdomen/clinical_description" label="Abdomen examination"></mb-input>
    <mb-input textarea path="gynaec_case_record_sidharth.v0/physical_examination_findings/pelvic/clinical_description" label="Pelvic examination"></mb-input>
</div>

<h2 class="text-xl font-semibold mb-4 mt-8">Urinanalysis</h2>
<div class="grid grid-cols-3 gap-4">
    <div>
        <mb-select path="gynaec_case_record_sidharth.v0/urinalysis/point_in_time:0/glucose" label="Glucose" terminology="undefined">
            <mb-option value="at0115" label="Negative" ordinal="1" ></mb-option>
            <mb-option value="at0116" label="Trace" ordinal="2" ></mb-option>
            <mb-option value="at0117" label="1+" ordinal="3" ></mb-option>
            <mb-option value="at0118" label="2+" ordinal="4" ></mb-option>
            <mb-option value="at0119" label="3+" ordinal="5" ></mb-option>
            <mb-option value="at0120" label="4+" ordinal="6" ></mb-option>
        </mb-select>
    </div>
    <div>
        <mb-select path="gynaec_case_record_sidharth.v0/urinalysis/point_in_time:0/ketones" label="Ketones" terminology="undefined">
            <mb-option value="at0109" label="Negative" ordinal="1" ></mb-option>
            <mb-option value="at0110" label="Trace" ordinal="2" ></mb-option>
            <mb-option value="at0111" label="Small" ordinal="3" ></mb-option>
            <mb-option value="at0112" label="Moderate" ordinal="4" ></mb-option>
            <mb-option value="at0113" label="Large" ordinal="5" ></mb-option>
            <mb-option value="at0114" label="Large+" ordinal="6" ></mb-option>
        </mb-select>
    </div>
    <div>
        <mb-select path="gynaec_case_record_sidharth.v0/urinalysis/point_in_time:0/blood" label="Blood" terminology="undefined">
            <mb-option value="at0102" label="Negative" ordinal="1" ></mb-option>
            <mb-option value="at0103" label="Non-haemolysed Trace" ordinal="2" ></mb-option>
            <mb-option value="at0104" label="Non-haemolysed Moderate" ordinal="3" ></mb-option>
            <mb-option value="at0105" label="Haemolysed Trace" ordinal="4" ></mb-option>
            <mb-option value="at0106" label="1+" ordinal="5" ></mb-option>
            <mb-option value="at0107" label="2+" ordinal="6" ></mb-option>
            <mb-option value="at0108" label="3+" ordinal="7" ></mb-option>
        </mb-select>
    </div>
    <div>
        <mb-select path="gynaec_case_record_sidharth.v0/urinalysis/point_in_time:0/ph" label="pH" terminology="undefined">
            <mb-option value="at0127" label="5.0" ordinal="1" ></mb-option>
            <mb-option value="at0128" label="5.5" ordinal="2" ></mb-option>
            <mb-option value="at0129" label="6.0" ordinal="3" ></mb-option>
            <mb-option value="at0130" label="6.5" ordinal="4" ></mb-option>
            <mb-option value="at0131" label="7.0" ordinal="5" ></mb-option>
            <mb-option value="at0132" label="7.5" ordinal="6" ></mb-option>
            <mb-option value="at0133" label="8.0" ordinal="7" ></mb-option>
            <mb-option value="at0134" label="8.5" ordinal="8" ></mb-option>
            <mb-option value="at0176" label="9.0" ordinal="9" ></mb-option>
            <mb-option value="at0177" label="9.5" ordinal="10" ></mb-option>
            <mb-option value="at0179" label="10.0" ordinal="11" ></mb-option>
        </mb-select>
    </div>
    <div>
        <mb-select path="gynaec_case_record_sidharth.v0/urinalysis/point_in_time:0/protein" label="Protein" terminology="undefined">
            <mb-option value="at0096" label="Negative" ordinal="1" ></mb-option>
            <mb-option value="at0097" label="Trace" ordinal="2" ></mb-option>
            <mb-option value="at0098" label="1+" ordinal="3" ></mb-option>
            <mb-option value="at0099" label="2+" ordinal="4" ></mb-option>
            <mb-option value="at0100" label="3+" ordinal="5" ></mb-option>
            <mb-option value="at0101" label="4+" ordinal="6" ></mb-option>
        </mb-select>
    </div>
</div>

<h2 class="text-xl font-semibold mb-4 mt-8">Blood Pressure</h2>
<div class="flex items-center w-64">
    <mb-quantity default="mm[Hg]" hideunit path="gynaec_case_record_sidharth.v0/blood_pressure/systolic">
        <mb-unit unit="mm[Hg]" label="mm[Hg]" min="" max="1000"></mb-unit>
    </mb-quantity>
    <span class="text-2xl font-bold mx-2 text-gray-400">/</span>
    <mb-quantity default="mm[Hg]" hideunit path="gynaec_case_record_sidharth.v0/blood_pressure/diastolic">
        <mb-unit unit="mm[Hg]" label="mm[Hg]" min="" max="1000"></mb-unit>
    </mb-quantity>
</div>

<mb-context path="gynaec_case_record_sidharth.v0/blood_pressure/time"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/blood_pressure/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/blood_pressure/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/blood_pressure/subject"></mb-context>

<mb-context path="gynaec_case_record_sidharth.v0/urinalysis/point_in_time:0/time"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/urinalysis/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/urinalysis/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/urinalysis/subject"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/physical_examination_findings/general/system_or_structure_examined" label="System or structure examined" bind={"General"} ></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/physical_examination_findings/abdomen/system_or_structure_examined" label="System or structure examined" bind={"Abdomen"} ></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/physical_examination_findings/pelvic/system_or_structure_examined" label="System or structure examined" bind={"Pelvic"} ></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/physical_examination_findings/time"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/physical_examination_findings/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/physical_examination_findings/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/physical_examination_findings/subject"></mb-context>