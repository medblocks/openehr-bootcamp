  <div class="grid grid-cols-2 gap-4">
    <div>
      <mb-buttons path="gynaec_case_record_sidharth.v0/sexual_health_summary/status" label="Status" terminology="local">
        <mb-option value="at0009" label="Sexually active, regular partner"></mb-option>
        <mb-option value="at0010" label="Sexually active, no regular partner"></mb-option>
        <mb-option value="at0011" label="Never sexually active"></mb-option>
      </mb-buttons>
    </div>
    <div>
      <mb-duration year path="gynaec_case_record_sidharth.v0/sexual_health_summary/first_ever_sex" label="First ever sex"></mb-duration>
    </div>
  </div>
<mb-context path="gynaec_case_record_sidharth.v0/sexual_health_summary/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/sexual_health_summary/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/sexual_health_summary/subject"></mb-context>

<h2 class="text-xl font-semibold mb-4 mt-8">Menstruation Summary</h2>
<mb-input textarea path="gynaec_case_record_sidharth.v0/menstruation_summary/overall_description" label="Overall description"></mb-input>
<div class="grid grid-cols-3 gap-4 mt-2">
  <div>
    <mb-duration year path="gynaec_case_record_sidharth.v0/menstruation_summary/menarche:0" label="Menarche"></mb-duration>
  </div>
  <div>
    <mb-buttons path="gynaec_case_record_sidharth.v0/menstruation_summary/per_episode/typical_pattern" label="Typical pattern" terminology="local">
      <mb-option value="at0015" label="Regular"></mb-option>
      <mb-option value="at0016" label="Irregular"></mb-option>
    </mb-buttons>
  </div>
  <div>
    <mb-date path="gynaec_case_record_sidharth.v0/last_menstrual_period/date_of_onset_lmp" label="Date of onset (LMP)"></mb-date>
  </div>
</div>
<mb-context path="gynaec_case_record_sidharth.v0/menstruation_summary/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/menstruation_summary/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/menstruation_summary/subject"></mb-context>

<mb-context path="gynaec_case_record_sidharth.v0/last_menstrual_period/language"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/last_menstrual_period/encoding"></mb-context>
<mb-context path="gynaec_case_record_sidharth.v0/last_menstrual_period/subject"></mb-context>