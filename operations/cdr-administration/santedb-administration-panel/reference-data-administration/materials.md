# Materials

{% hint style="info" %}
This page documents a SanteDB 3.0 Feature
{% endhint %}

In SanteDB and is derived products: SanteEMR, SanteIMS, etc. the concept of a [Material](https://help.santesuite.org/santedb/data-and-information-architecture/conceptual-data-model/entities/data-dictionary#material) is used to express any physical object which is used to deliver care. This includes:

* Types / Classifications of materials (see: [Determiner Codes](../../../../santedb/data-and-information-architecture/conceptual-data-model/entities/determiner-codes.md))
* &#x20;Manufactured types of materials (such a trade names, products, etc.)
* Lot numbers (individual orderable instances of the material)

Take, for example, the material of HPV - HPV is modeled in SanteDB as:

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Here:

* HPV Unspecified Formulation is a `Material` with a `DeterminerConcept` of `DescribedKind` and a code of `VaccineType-HPV` (linking to an unspecified formulation)
* Two Products are defined:
  * Guardasil4 10 Dose Vials is a `ManufacturedMaterial` with `DeterminerConcept` of `QualifiedKind,` a relationship of `ManufacturedProduct` with `Organization` `Pfizer` as the supplier/manufacturer, and a `Has Generalization` relationship with `Quantity` of 10 to the generic HPV (i.e. 1 Guardasil4 10 Dose Vial is 10 HPV Unspecified Formulation) and a `TypeConcept` of `VaccineType-HPV4`
  * Guardasil9 10 Dose Vials with the same linkages
* Two Lot numbers defined as:
  * Lot #0293 which is an instance of Guardasil4 10 Dose Vials
  * Lot #3982 which is an instance of Guardasil4 10 Dose Vials

To manage materials, administrators should use **Reference Data > Materials** this will present the administrator with a list of all top level material definitions in SanteDB.

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The administrator can use this screen to:

* **Create** a new material definition in the SanteDB instance
* **Export** the master material list as a dataset to be imported into another SanteDB instance
* **View** an existing registered material
* **Delete** or **UnDelete** a registered material

## Creating Materials

Creating a new material definition is accessed via the Material List. First the material core properties are configured

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



<table><thead><tr><th width="222">Field</th><th>Description</th></tr></thead><tbody><tr><td>Material Type</td><td>The type/classification of the material being created, this dictates the CVX code used when this material is represented on user interfaces.</td></tr><tr><td>Is Administrable</td><td>When selected, indicates that the material can be <strong>administered</strong> to a patient (examples: drugs, vaccines, etc.) when a material cannot be administered these are supportive materials (examples: syringes, diluents, etc.)</td></tr><tr><td>Official Name</td><td>The long-form, official name for the material.</td></tr><tr><td>Common Name</td><td>The short-form name used in summary reports and user interfaces</td></tr><tr><td>Form</td><td>The form code which the material takes on - this can be injection, pills, drops, applicators</td></tr><tr><td>Dose Unit</td><td>When the material is dosed or administered, the unit of measure to be used (examples: Dose, Milliliter, Deciliter, Bags, Puffs, Drops etc.)</td></tr><tr><td>Special Instructions</td><td>Any special instructions which are to be added to the material.</td></tr></tbody></table>

### Identification

Materials typically also carry one or more identifiers which are used for interoperability with logistics systems, and other trading partners.

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Depending on your deployment of SanteDB, there may be additional identifier types which are required to facilitate interoperability. Please consult your local deployment documentation.
{% endhint %}

### Extended Attributes

Additionally, the creation of a material may also specify additional extended attributes

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="158">Field</th><th>Description</th></tr></thead><tbody><tr><td>Parent</td><td>If the material is a child in a hierarchy of materials, then the parent may be specified here. For example, it is possible to create a material kind called <code>RoutineVitaminSupplement</code> which is a parent of <code>Vitamin K</code>, <code>Vitamin A</code>, etc.</td></tr><tr><td>Has Parts</td><td>If the material is a composite of other materials, the individual components of the materials should be listed here.</td></tr><tr><td>Bundled Materials</td><td>If the material is directly linked to other materials which are consumed as a result of consuming this material, they are listed here. For example, one dose of <code>BCG</code> consumes one dose of <code>BCG Diluent</code> which consumes one <code>ADS_0.05</code> syringe and a reconstitution syringe</td></tr><tr><td>Regulatory Body</td><td>If the material is a part of a regulation or approval process, then specify the regulatory bodies which are required to approve these materials.</td></tr><tr><td>Approved Treatment</td><td>If the material is used specifically for the treatment or prevention of one or more diseases, then list the diseases here. This can be used for more complex CDSS rules to determine full immunity for a specific disease.</td></tr></tbody></table>

## Material Details

The material details page shows all relevant information associated with the material including:

* Core properties of the material
* The relationships of one material to another
* Products and lot number associated with the material

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

Any of the data in the panels can be changed by selecting the edit option for the material panel.

### Bundling Materials

When a material is bundled with another, use the `Bundle Items` tab. Administrators should then select the material associated and the quantity of the material incuded. I.e. for every 1 of the current material _n_ of the linked material is used.

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Adding Products

To add a product to a material, select the **Products** tab. This will display a list of all products which are related to the current material.

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

A new product is created by selecting **Add** and entering the related material details.

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="207">Field</th><th>Description</th></tr></thead><tbody><tr><td>Manufacturer</td><td>The manufacturer of the material (the registered manufacturing organization in the SanteDB organization list)</td></tr><tr><td>Product Code</td><td>If the product has a more specific codification than the parent/generic material then the product code is specified.</td></tr><tr><td>Trade Name</td><td>The trade name of the material</td></tr><tr><td>GS1 GTIN</td><td>The GTIN which is used for ordering the product from the LMIS system</td></tr><tr><td>Contained Quantity</td><td>The number of the parent material which is contained in one instance of the product. For 5 dose vials this is <code>5</code> for 20 dose vials this is <code>20</code>, etc.</td></tr><tr><td>Stock Quantity</td><td>How this product is measured in your implementation of SanteDB. This can also be <code>Doses</code> or can be <code>Vials</code> or <code>Crates</code> or <code>Boxes</code></td></tr><tr><td>Batches/Lots</td><td>If you wish to pre-create a series of lot numbers and batches this may be done here</td></tr></tbody></table>

Administrators can delete products as well using the product screen.

{% hint style="info" %}
Deleting the Product also hides all associated lot numbers for that product, and prevents further syncrhonization to dCDR clients. It is recommended to use the status indiator instead.
{% endhint %}

### Adding Lot / Batch Numbers

Batches and lots can be added to the material via the **Lot Numbers** tab, which shows a summary of all lot numbers registered for the material.

<figure><img src="../../../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

To add a lot number, the **Add** option can be used, alternatively the **Edit** option can be used to edit a single instance of the batch.

<figure><img src="../../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>
