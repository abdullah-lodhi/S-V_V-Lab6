### Variable Definitions
| Variable Name | Data Type | Description |
|---|---|---|
| R_open | Boolean | The crossing is open to road traffic. |
| T_approach | Boolean | A train is approaching the crossing. |
| E_emergency | Boolean | An emergency condition exists. |
| T_detect | Boolean | The system has detected an approaching train. |
| W_warn | Boolean | The warning lights and siren are active. |
| B_lower | Boolean | The barrier is fully lowered and locked. |
| B_open | Boolean | The barrier is open. |
| T_clear | Boolean | The train has fully cleared the crossing. |
| Track_safe | Boolean | The track is confirmed safe. |
| Sensor_fail | Boolean | A track sensor has failed or reports inconsistent data. |
| Safe_fallback | Boolean | The system has entered a safe fallback state. |
| Alarm_raise | Boolean | The alarm has been raised. |
| W_control | Boolean | Warning controls are available. |
| B_control | Boolean | Barrier controls are available. |
| U_unsafe | Boolean | The crossing is treated as unsafe. |
| O_clear | Boolean | The obstacle sensor indicates the crossing is clear. |
| Alarm_operator | Boolean | The operator alarm is active. |

### Formalized Constraints
| Constraint ID | Description (Simple English) | Formal Logical Expression |
|---|---|---|
| C1 | The crossing must remain open to road traffic when no train is approaching and no emergency condition exists. | (¬T_approach ∧ ¬E_emergency) → R_open |
| C2 | The system must detect a train approaching before it reaches the danger zone. | T_approach → T_detect |
| C3 | Once a train is detected approaching, the warning lights and siren must activate. | T_detect → W_warn |
| C4 | The barrier must lower fully and lock before a train enters the crossing. | T_detect → B_lower |
| C5 | The barrier must open only after the train has cleared the crossing and the track is confirmed safe. | B_open → (T_clear ∧ Track_safe) |
| C8 | If a track sensor fails or reports inconsistent data, the system must trigger a safe fallback state and raise an alarm. | (Sensor_fail) → (Safe_fallback ∧ Alarm_raise) |
| C11 | If both warning and barrier controls are unavailable, the crossing must be treated as unsafe and the operator must be alarmed. | (¬W_control ∧ ¬B_control) → (U_unsafe ∧ Alarm_operator) |
| C15 | The barrier must not open while a train is approaching, even if the obstacle sensor indicates the crossing is clear. | (T_approach ∧ O_clear) → ¬B_open |
