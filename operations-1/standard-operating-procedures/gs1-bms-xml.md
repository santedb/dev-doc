# GS1 BMS XML

SanteDB provides a basic implementation of the [GS1 Business Messaging Standard (BMS) 3.3](https://www.gs1.org/standards/gs1-xml/guideline/ediint-as1-and-as2-transport-communication-guidelines) for conveying stock transactions to logistics systems.

{% hint style="warning" %}
The SanteDB GS1 BMS interfaces are undergoing refactoring from OpenIZ. The information in these pages document the OpenIZ GS1 plugin that is currently ported to SanteDB however has not been validated.
{% endhint %}

## GS1 Stock Messaging Workflows

The overall order flow in SanteDB follows the order flow in GS1:&#x20;

1. An order is created in SanteDB (a `Request for Supply Act` ) which is stored with product classes and quantities requested.
2. SanteDB's iCDR constructs a `Order` message and sends it to the supplier
3. The supplier validates the order and responds to SanteDB with an `OrderResponse` which is linked in SanteDB (a `Promise to Supply` which `Fulfills` the `Request for Supply`)
4. The supplier picks and packs the order and despatches the order sending SanteDB with actual product (GTIN and LOT#) via a `DespatchAdvice` , SanteDB stores the order in RIM (a `EventOccurence Supply` which documents `Departure` of the `Promise for Supply`)
5. The product arrives at the clinic, the clinic staff count and verify the product and confirm receipt (a `EventOccurrence of Supply` which documents `Arrival` of the `EventOccurence Supply`)&#x20;
6. SanteDB's iCDR constructs a `ReceiveAdvice` message and sends it to the supplier.&#x20;

### Order Flow

The order flow is triggered whenever a client of the iCDR submits an `Act` with mood code `Request` and a type of `Supply` (i.e. Request for Supply). When configured, the iCDR will construct a GS1 [`Order` message](https://www.gs1.org/standards/edi-xml/xml-order/3-4-1) and will issue the message over `AS.2` over HTTP with mime encoded attachment or can perform a simple `POST` with the order message as the request.

The logistics management information system may perform an internal approval of the order and can accept the order (with modifications to the quantities) via a [GS1 Order Response](https://www.gs1.org/standards/edi-xml/xml-order-response/3-4-1).

![](<../../.gitbook/assets/image (409).png>)

The order and order response is made up of a series of `tradeItemDetail` which are mapped to the  `Product` participations in the original `Supply` request (these are typically `Materials`). If an order response is set then the iCDR creates a new `Act` with mood-code of `Promise` linking the new act with the request act as a `Fulfills` relationship.

For example, an order request from Elbonia's Good Health Hospital:

```markup
<?xml version="1.0"?>
<orderMessage xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="urn:gs1:ecom:order:xsd:3">
  <StandardBusinessDocumentHeader xmlns="http://www.unece.org/cefact/namespaces/StandardBusinessDocumentHeader">
    <HeaderVersion>1.0</HeaderVersion>
    <Sender>
      <!-- Truncated -->
    </Sender>
    <DocumentIdentification>
      <Standard>GS1</Standard>
      <TypeVersion>3.3</TypeVersion>
      <InstanceIdentifier>44432A5701A4F209</InstanceIdentifier>
      <Type>order</Type>
      <MultipleType>false</MultipleType>
      <CreationDateAndTime>2020-11-12T01:30:49.4634744-08:00</CreationDateAndTime>
    </DocumentIdentification>
  </StandardBusinessDocumentHeader>
  <order xmlns="">
    <creationDateTime>2020-11-12T01:30:46.219541</creationDateTime>
    <documentStatusCode>ORIGINAL</documentStatusCode>
    <orderIdentification>
      <entityIdentification>2227710f-5b6a-49ea-893e-13bb483b2cf4</entityIdentification>
    </orderIdentification>
    <isApplicationReceiptAcknowledgementRequired>true</isApplicationReceiptAcknowledgementRequired>
    <isOrderFreeOfExciseTaxDuty>false</isOrderFreeOfExciseTaxDuty>
    <orderLogisticalInformation>
      <shipTo>
        <additionalPartyIdentification additionalPartyIdentificationTypeCode="HIE_FRID">urn:uuid:b2955791-ea33-3048-a438-866188819d7f</additionalPartyIdentification>
        <address>
          <street>23 Main Street</street>
          <city>Muddsville</city>
          <countryCode>ELB</countryCode>
          <state>MU</state>
        </address>
        <organisationDetails>
          <organisationName>Good Health Hospital</organisationName>
        </organisationDetails>
      </shipTo>
      <orderLogisticalDateInformation>
        <requestedDeliveryDateTime>
          <date>2020-11-12</date>
        </requestedDeliveryDateTime>
      </orderLogisticalDateInformation>
    </orderLogisticalInformation>
    <orderLineItem>
      <lineItemNumber>1</lineItemNumber>
      <requestedQuantity measurementUnitCode="dose" codeListVersion="UCUM">20</requestedQuantity>
      <additionalOrderLineInstruction languageCode="en">FRAGILE</additionalOrderLineInstruction>
      <additionalOrderLineInstruction languageCode="en">KEEP REFRIGERATED</additionalOrderLineInstruction>
      <transactionalTradeItem>
        <tradeItemDescription>HPV</tradeItemDescription>
        <itemTypeCode codeListVersion="CVX">137</itemTypeCode>
        <tradeItemClassification>
          <additionalTradeItemClassificationCode codeListVersion="VIMS_ITEM_ID">2429</additionalTradeItemClassificationCode>
        </tradeItemClassification>
      </transactionalTradeItem>
    </orderLineItem>
    <!-- Repeat orderLineItem -->
  </order>
</orderMessage>
```

### Order Despatch

Once the order is approved by the LMIS / Distributor it is expected that the requested order will be picked and packed. Once the order has been despatched (i.e. it is on a truck, or courier, etc.) the LMIS will respond with a [GS1 Despatch Advice](https://www.gs1.org/standards/edi-xml/xml-despatch-advice/3-4-1-0) message.

The `Despatch Advice` differs from the `Order` message in that it contains:

* The actual quantity of each item packed and shipped
* The actual product codes (GTIN) and lot #'s of products shipped
* The expected date of delivery (EDD)

The iCDR converts this into an `Act` with class code of `Supply` , mood code of `EventOccurence` and a status of `Active`, dCDRs will synchronize this from the core iCDR model on their next synchronization, or clients may request the information in any of the supported iCDR messaging formats. The new `Act` is linked to the original `Act` with an `ActRelationship` carrying relationship type of `Fulfills` (i.e. the new act fulfills the request act)

![](<../../.gitbook/assets/image (408).png>)

#### Orderless Despatch

In some jurisdictions stock is sent without explicit ordering to a facility. These orderless despatches are supported by SanteDB and are implemented as a GS1 `DespatchAdvice` message with no source order information.&#x20;

### Order Receive

Once an order is received by the remote facility or original caller, the user will open the package and will verify the contents. This may include:

* Verifying the quantities of stock shipped
* Verifying the cold storage status (VVM) of any vials of product shipped
* Identifying breakage and items to be rejected.

The caller creates a new `Act` with class code `Supply` with status code of `Complete` and mood code of `EventOccurence`. The created act is linked to the despatched act with an `ActRelationship` carrying type `Arrival` (i.e. the new act documents the arrival of the previous act).&#x20;

The previous act has its status code set to `Complete` .

![](<../../.gitbook/assets/image (407).png>)

For example, an order receive message for Good Health Hospital may appear as:

```markup
<?xml version="1.0"?>
<receivingAdviceMessage xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="urn:gs1:ecom:receiving_advice:xsd:3">
  <StandardBusinessDocumentHeader xmlns="http://www.unece.org/cefact/namespaces/StandardBusinessDocumentHeader">
    <HeaderVersion>1.0</HeaderVersion>
    <Sender>
      <!-- Truncated -->
    </Sender>
    <DocumentIdentification>
      <Standard>GS1</Standard>
      <TypeVersion>3.3</TypeVersion>
      <InstanceIdentifier>4281C212207220B2</InstanceIdentifier>
      <Type>receivingAdvice</Type>
      <MultipleType>false</MultipleType>
      <CreationDateAndTime>2020-12-16T23:04:53.7368109-08:00</CreationDateAndTime>
    </DocumentIdentification>
  </StandardBusinessDocumentHeader>
  <receivingAdvice xmlns="">
    <creationDateTime>2020-12-16T05:21:07.118676</creationDateTime>
    <documentStatusCode>ORIGINAL</documentStatusCode>
    <receivingAdviceIdentification>
      <entityIdentification>4bb1d8cd-d8d6-4531-be43-189661b7a1db</entityIdentification>
    </receivingAdviceIdentification>
    <receivingDateTime>2020-12-16T05:21:03.764</receivingDateTime>
    <reportingCode>FULL_DETAILS</reportingCode>
    <shipper>
      <additionalPartyIdentification additionalPartyIdentificationTypeCode="HIE_FRID">urn:uuid:9b573dd9-1e72-3110-9540-8b7cd1a59df4</additionalPartyIdentification>
      <address>
        <countryCode>ELB</countryCode>
        <state>MU</state>
      </address>
      <organisationDetails>
        <organisationName>Muddsville Regional Distribution Centre</organisationName>
      </organisationDetails>
    </shipper>
    <receiver>
      <additionalPartyIdentification additionalPartyIdentificationTypeCode="HIE_FRID">urn:uuid:04333219-4f77-3a16-947f-b52527b54453</additionalPartyIdentification>
      <address>
        <street>23 Main Street</street>
        <city>Muddsville</city>
        <countryCode>ELB</countryCode>
        <state>MU</state>
      </address>
      <organisationDetails>
        <organisationName>Good Health Hospital</organisationName>
      </organisationDetails>
    </receiver>
    <shipTo>
      <!-- Truncated -->
    </shipTo>
    <despatchAdvice>
      <entityIdentification>a905c25c-47ac-4775-a7be-0498cbeef3cf</entityIdentification>
      <creationDateTime>2020-09-29T08:54:24.898187</creationDateTime>
    </despatchAdvice>
    <receivingAdviceLogisticUnit>
      <receivingAdviceLineItem>
        <lineItemNumber>1</lineItemNumber>
        <quantityAccepted measurementUnitCode="each" codeListVersion="UCUM">80</quantityAccepted>
        <quantityDespatched measurementUnitCode="each" codeListVersion="UCUM">80</quantityDespatched>
        <transactionalTradeItem>
          <gtin>10060123AD</gtin>
          <tradeItemDescription>BCG Diluent (Serum Institute of India)</tradeItemDescription>
          <itemTypeCode codeListVersion="OpenIZ-MaterialType">62962d65-be7b-465d-9a92-772ea3ba0d03</itemTypeCode>
          <transactionalItemData>
            <batchNumber>068S14079Z</batchNumber>
            <itemExpirationDate>2021-03-31</itemExpirationDate>
          </transactionalItemData>
        </transactionalTradeItem>
        <receivingConditionInformation>
          <receivingConditionCode>DAMAGED_PRODUCT_OR_CONTAINER</receivingConditionCode>
          <receivingConditionQuantity measurementUnitCode="each" codeListVersion="UCUM">0</receivingConditionQuantity>
        </receivingConditionInformation>
        <receivingConditionInformation>
          <receivingConditionCode>GOOD_CONDITION</receivingConditionCode>
          <receivingConditionQuantity measurementUnitCode="each" codeListVersion="UCUM">80</receivingConditionQuantity>
        </receivingConditionInformation>
      </receivingAdviceLineItem>
    </receivingAdviceLogisticUnit>
    <!-- Repeat for each Accepted Item -->
  </receivingAdvice>
</receivingAdviceMessage>
```
