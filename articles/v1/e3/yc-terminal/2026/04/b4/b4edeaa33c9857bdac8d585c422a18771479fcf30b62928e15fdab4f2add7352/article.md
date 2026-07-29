---
schema_version: "1.0.0"
document_id: "b4edeaa33c9857bdac8d585c422a18771479fcf30b62928e15fdab4f2add7352"
company_key: "yc-terminal"
company: "Terminal"
source_id: "yc-terminal-rss-78690d64b189"
canonical_url: "https://docs.withterminal.com/changelog"
published_at: "2026-04-10T14:44:53+00:00"
first_seen_at: "2026-07-26T01:53:49.682680+00:00"
fetched_at: "2026-07-29T15:29:54.465734+00:00"
content_hash: "sha256:8a897010e0a8c4263cafd0a19ca0ed52f3b8e28e29c7c6c452ff195ee729ebdc"
---

# 2026-04-10

### New Integrations


- [GPS Trackit](https://docs.withterminal.com/providers/tsp/gps-trackit)
- [Zonar Ignition](https://docs.withterminal.com/providers/tsp/zonar-ignition)


### Integration Updates


- [Geotab](https://docs.withterminal.com/providers/tsp/geotab) now supports additional[Safety Events](https://docs.withterminal.com/models/safety-event) :` camera_obstruction` ,` cell_phone` ,` distracted` ,` drowsiness` ,` eating_and_drinking` ,` near_crash` ,` rolling_stop` ,` smoking` , and` tailgating`
- [Loop ELD](https://docs.withterminal.com/providers/tsp/loop-eld) now supports[Historical Vehicle Locations](https://docs.withterminal.com/models/vehicle-location) and[HOS Available Time](https://docs.withterminal.com/api-reference/hours-of-service/list-hosavailable-time)
- [Omnitracs ES](https://docs.withterminal.com/providers/tsp/omnitracs-es) now supports[Vehicle Utilization](https://docs.withterminal.com/models/vehicle-utilization-day)


### Dashboard Updates


- Improved similar connection suggestions in the[Terminal Dashboard](https://dashboard.withterminal.com/) to make duplicate connection detection clearer


### Consent Flow Updates


- Added stricter validation for required external IDs in Link to prevent invalid connection requests earlier in onboarding


### Documentation Updates


- Clarified sandbox access in[Getting Started](https://docs.withterminal.com/introduction)
- Expanded provider model support status guidance in provider documentation
