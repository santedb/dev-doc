# HL7v2

SanteDB support for HL7v2 messaging is implemented via `Hl7MessageHandler` daemon service in the `SanteDB.Message.HL7.dll` assembly. When enabled, the HL7v2 interface will process inbound messages by matching their trigger event and message type to a registered `IHL7MessageHandler` instance.

## Processing of HL7 Messages

When an inbound message is received via any registered transport, the following process is initiated:

1. The incoming message socket is consumed, if the message is received via SLLP then the client certificate is amended to the message receive event.
2. The message is converted to HL7v2.5 which is the canonical version of HL7 used within SanteDB for all handlers.
3. The `MSH-9` field is read and an applicable `IHl7MessageHandler` instance is located based on the trigger event.
4. The message handler authenticates the sender by:
   1. Using the client certificate information provided by the sending system, 
   2. Using the `MSH-3` and `MSH-4` fields and the `MSH-8` security value to authenticate the sending application/device,
   3. Optionally the `SFT-2` value is used to authenticate application
5. The message handler iterates over the segments and segment groups and calls `IHl7SegmentHAndler` instances to parse the message
6. The message handler performs the necessary actions based on the incoming message
7. The message handler returns a `Bundle` instance which the processor \(again\) calls `IHl7SegmentHandler` instances to parse the RIM based objects back into HL7v2
8. The server appends the necessary sending information and message metadata, 
9. The response is sent via the same channel it was received

