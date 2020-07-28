# Null Reasons

Whenever submitting data to SanteDB's CDR where an element is marked as required, you may submit a null reason \(also known as a null flavor\). The allowed null flavors are:U

| Mnemonic | Description |
| :--- | :--- |
| AskedUnknown | The value was asked for, however the known value could not be collected. |
| Derived | The value was not supplied because it can be calculated from other data provided. |
| Invalid | The value was not supplied because the known value would violate business rules. |
| Masked | The value is not supplied because the value is sensitive and disclosure may violate privacy. |
| NotApplicable | The value is not supplied because it is not applicable \(for example: Last menstrual period for a man\) |
| NotAsked | The value is not supplied because it was not asked for. |
| Unavailable | The value is not available at the time of data capture. |
| NoInformation | The value is not supplied because there is no information supplied. This is the default null flavor to use. |
| NegativeInfinity | The value is not supplied because it is negative infinity. |
| Other | The value was not supplied for some other reason. |
| PositiveInfinity | The value was not supplied because it is positive infinity. |
| SufficientQuantity | The value is of sufficient quantity to meet a clinical trigger, however the exact value could not be measured \(i.e. off-scale 0 or off-scale max\) |
| Trace | The value is above 0, however the exact value is unknown or the equipment could not measure the quantity. |
| UnEncoded | The value could not be encoded into the message. |
| Unknown | The value is unknown \(not asked, not measured, etc.\) |

