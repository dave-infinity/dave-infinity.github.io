---
id: 239
title: 'Dynamic MySQL View for Calculated fields'
date: '2014-07-16T11:51:13+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=239'
permalink: /2014/07/dynamic-mysql-view-for-calculated-fields/
categories:
    - MySQL
tags:
    - calculated
    - dynamic
    - mysql
    - view
---

the field on it’s own:  
SELECT IF(z.ts\_mon\_journeys \* (SELECT tsm\_mileage from time\_sheet\_mileage where tsm\_user=’MinHourPerJourney’) &gt; IfNull(z.ts\_mon\_hours,0), z.ts\_mon\_journeys \* (SELECT tsm\_mileage from time\_sheet\_mileage where tsm\_user=’MinHourPerJourney’), z.ts\_mon\_hours) TotalHours

mileagecosts:  
(journeys \* mileageforuser) \* pricepermile  
(IfNull(z.ts\_mon\_journeys,0) \* (SELECT y.tsm\_mileage from time\_sheet\_mileage y where y.tsm\_user=z.ts\_userid)) \* (SELECT tsr\_payment\_rate from time\_sheet\_rates WHERE tsr\_call\_out\_code=’PricePerMile’) MileageCosts

FINAL STATEMENT:  
``

```

CREATE VIEW time_sheet_calc_dynamic As SELECT z.ts_id, 
IfNull(z.ts_mon_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) MonMileage, 
IfNull((SELECT tsr_payment_rate from time_sheet_rates where time_sheet_rates.tsr_call_out_code=z.ts_mon_standby),0) MonStandbyRate, 
IfNull((SELECT IF(z.ts_mon_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_mon_hours,0), z.ts_mon_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_mon_hours)),0) MonTotalHours, 
(IfNull(z.ts_mon_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") MonMileageCosts,
IfNull(z.ts_tue_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) TueMileage,
IfNull((SELECT tsr_payment_rate from time_sheet_rates where time_sheet_rates.tsr_call_out_code=z.ts_Tue_standby),0) TueStandbyRate,
IfNull((SELECT IF(z.ts_Tue_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_Tue_hours,0), z.ts_Tue_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_Tue_hours)),0) TueTotalHours,
(IfNull(z.ts_Tue_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") TueMileageCosts,

IfNull(z.ts_wed_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) wedMileage,
IfNull((SELECT tsr_payment_rate from time_sheet_rates where time_sheet_rates.tsr_call_out_code=z.ts_wed_standby),0) wedStandbyRate,
IfNull((SELECT IF(z.ts_wed_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_wed_hours,0), z.ts_wed_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_wed_hours)),0) wedTotalHours,
(IfNull(z.ts_wed_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") wedMileageCosts,

IfNull(z.ts_thu_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) thuMileage,
IfNull((SELECT tsr_payment_rate from time_sheet_rates where time_sheet_rates.tsr_call_out_code=z.ts_thu_standby),0) thuStandbyRate,
IfNull((SELECT IF(z.ts_thu_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_thu_hours,0), z.ts_thu_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_thu_hours)),0) thuTotalHours,
(IfNull(z.ts_thu_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") thuMileageCosts,

IfNull(z.ts_fri_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) friMileage,
IfNull((SELECT tsr_payment_rate from time_sheet_rates where time_sheet_rates.tsr_call_out_code=z.ts_fri_standby),0) friStandbyRate,
IfNull((SELECT IF(z.ts_fri_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_fri_hours,0), z.ts_fri_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_fri_hours)),0) friTotalHours,
(IfNull(z.ts_fri_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") friMileageCosts,

IfNull(z.ts_sat_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) satMileage,
IfNull((SELECT IF(z.ts_sat_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_sat_hours,0), z.ts_sat_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_sat_hours)),0) satTotalHours,
(IfNull(z.ts_sat_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") satMileageCosts,

IfNull(z.ts_sun_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) sunMileage,
IfNull((SELECT IF(z.ts_sun_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_sun_hours,0), z.ts_sun_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_sun_hours)),0) sunTotalHours,
(IfNull(z.ts_sun_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") sunMileageCosts,

IfNull(z.ts_mam_journeys,0) * IfNull((SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid),0) mamMileage,
IfNull((SELECT IF(z.ts_mam_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney") > IfNull(z.ts_mam_hours,0), z.ts_mam_journeys * (SELECT tsm_mileage from time_sheet_mileage where tsm_user="MinHourPerJourney"), z.ts_mam_hours)),0) mamTotalHours,
(IfNull(z.ts_mam_journeys,0) * (SELECT y.tsm_mileage from time_sheet_mileage y where y.tsm_user=z.ts_userid)) * (SELECT tsr_payment_rate from time_sheet_rates WHERE tsr_call_out_code="PricePerMile") mamMileageCosts,

z.ts_ts


FROM time_sheet z WHERE z.ts_calculation_completed1 or IsNull(z.ts_calculation_completed) ; 
```