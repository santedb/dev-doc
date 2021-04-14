# Entity Relationships

Figure 2 represents a sample information model of a kit of BCG vaccine. The model illustrates how a single tuples in the SanteDB model are related to one another to represent a kit. The material “BCG Vaccine” is comprised of one dose of “BCG Antigen”, one “Syringe”, and one dose of “BCG Diluent”. A box of “BCG Vaccine” represents 25 single doses of “BCG Vaccine” \(meaning 25 syringes, 25 antigen and 25 diluent\). Finally, from this we can order \(via instantiation or inheriting a kind\) a kit of GSK 5ml BCG vaccine. This derivation will have the same rules applied \(in that this vaccine must have a syringe, antigen, and diluent.

![Figure 2 - Kitting of BCG](../../../../../.gitbook/assets/image%20%2859%29.png)

Figure 3 represents a complex scenario of kitting a vaccine and then deriving a specific type of kit. The relationship between the instantiation and the generic concepts of the material would have a type of “Manufactured” meaning the “GSK 5 ml BCG” is a manufactured representation of the generic BCGvaccine.

![Figure 3 - Instantiating BCG Vaccine kit to Manufactured Materials ](../../../../../.gitbook/assets/image%20%281%29.png)

The SanteDB model also supports more simplistic representation of a “BCG Vaccine” if kits are not required by the jurisdiction that is implementing SanteDB. Figure 4 illustrates a valid representation of BCG in a jurisdiction where only the antigen is tracked.

![Figure 4 - Representing an instance of a KIND of Entity](../../../../../.gitbook/assets/image%20%2853%29.png)

### Type and Classification

An entity relationship has two codes which dictate the nature of the relationship between the holder \(the entity which owns the relationship\) and the target \(the entity to which the holder is related\). These are the relationshipType and the classificationType.

The relationshipType dictates the primary nature of the relationship, or the role that the target plays in related to the holder. Common relationship types are listed below \(the full set is derived from the Concept Set `EntityRelationshipType`\).

<table>
  <thead>
    <tr>
      <th style="text-align:left">Relationship Type</th>
      <th style="text-align:left">Use</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Family Members (Mother, Father,
        <br />Sister, Brother, Sibling, etc.)</td>
      <td style="text-align:left">
        <p>Indicates that the target has a familial relationship with the</p>
        <p>holder. In these relationships the target IS A (mother, father, etc.)</p>
        <p>to the holder.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Parent / Child</td>
      <td style="text-align:left">
        <p>Indicates that the target is a parent or the target is a child of the</p>
        <p>holder.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>DedicatedServiceDeliveryLocation,</p>
        <p>ServiceDeliveryLocation</p>
      </td>
      <td style="text-align:left">Indicates that the target is the primary facility at which services are
        rendered for the holder.</td>
    </tr>
    <tr>
      <td style="text-align:left">Replaces</td>
      <td style="text-align:left">The target replaces the holder</td>
    </tr>
  </tbody>
</table>

The classification of the relationship indicates the nature of the target in relation to the holder. The classification is derived from `RelationshipClass.` If a classification is not specified, then it is assumed the relationship  is not classified caller to interpret the context.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Classification Type</th>
      <th style="text-align:left">Use</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ContainedObjectLink</td>
      <td style="text-align:left">
        <p>Indicates that the target object adds further context to the holder,</p>
        <p>and that the contained object should not be used on its own without</p>
        <p>context of the holder.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ReferenceObjectLink</td>
      <td style="text-align:left">
        <p>Indicates that the target object is merely a reference of an independently</p>
        <p>submitted source object. These relationships classifications are used,
          for example, when the target was submitted and can exist independently
          of the holder (could be in the same same transaction)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PrivateLink</td>
      <td style="text-align:left">Indicates that the relationship was established for a system purpose,
        and not by a user or calling solution. Private links are used by the MDM
        layer, the matching layer, and others to indicate a &quot;do not remove&quot;
        condition to the persistence layer (i.e. the MDM layer has established
        this relationship and only the MDM layer can remove it).</td>
    </tr>
    <tr>
      <td style="text-align:left">PublicContactLink</td>
      <td style="text-align:left">Indicates that the holder and the target have a direct contact link, that
        is that the calling system (or an end user using the calling system) may
        use the relationship to directly contact the source. This is used often
        in the HL7v2 and FHIR layer for &quot;contacts&quot; (i.e. Mother relationship
        which can be Contacted)</td>
    </tr>
  </tbody>
</table>



