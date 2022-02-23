---
description: Patient Identity Feed – Full patient record
---

# TEST: OHIE-CR-08-HL7v2

This test ensures that the receiver is able to store and usefully convey (regurgitate) a more complete patient record having multiple names, addresses, telephone numbers, mother’s identifier, mother’s name, birth date, multiple birth order, etc.

## References

## Pre-Conditions / Setup

#### Setup the receiver such that OID 2.16.840.1.113883.3.72.5.9.1 has assigning authority of TEST which can be assigned from TEST\_HARNESS

## Test Step 1:

Test harness sends an ADT^A01 message with complex data set.

```
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451||ADT^A01^ADT_A01|TEST-CR-08-10|P|2.3.1
EVN||20101020
PID|||RJ-442^^^TEST||FOSTER^FANNY^FULL^^^^L|FOSTER^MARY^^^^^L|1970|F|||123 W34 St^^FRESNO^CA^30495||^PRN^PH^^^419^31495|^^PH^^^034^059434|EN|S|||||
PV1||I
```

### Expected Behaviour

* Receiver Accepts Message with an AA
* MSH-5 and MSH-6 matches “TEST\_HARNESS|TEST”

## Test Step 2:

Test harness verifies demographics data matches by executing a PDQ query with the patient’s identifier.

```
MSH|^~\&|TEST_HARNESS|TEST|CR1|MOH_CAAT|20090226131520-0600||QBP^Q22^QBP_Q21|TEST-CR-08-30|P|2.5
QPD|Q22^Find Candidates^HL7|Q0740|@PID.3.1^RJ-442~@PID.3.4.1^TEST
RCP|I|10^RD
```

### Expected Behaviour

* Receiver responds with an AA
* Receiver sends exactly one PID segment with identifier RJ-442 in domain TEST in PID-3
* Receiver sends:
  * PID-5=FOSTER^FANNY^FULL^^^^L
  * PID-6=FOSTER^MARY^^^^^L
  * PID-7=1970
  * PID-8=F
  * PID-11=123 W34 St^^FRESNO^CA^20495
  * PID-13=^PRN^PH^^^419^31495
  * PID-14=^^PH^^^034^059434
  * PID-15=EN
  * PID-16=S
