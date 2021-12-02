# Dataset Files

Sometimes your plugin/applet will need to include specialized data in order to operate. Some examples of data which a plugin might rely on are:

* New Concepts and ReferenceTerms for standardized vocabulary
* New Materials and ManufacturedMaterials which are used/distributed by the application
* New Places or Organizations which support a particular plugin.

### Dataset Files

All data in SanteDB's datastore can be distributed in the form of a data set. A data set file is a special file which contains a series of RIM objects (serialized in HDSI XML format) and instructions on how the RIM object should be treated.

Dataset files should be placed in the **data/** folder of your applet (if you're distributing via applet) or should be copied into the **data/** folder of the SanteDB server on installation (if you're distributing via .NET installer).

The structure of a dataset file is as follows:

```markup
<?xml version="1.0" encoding="utf-8" ?>
<dataset xmlns="http://santedb.org/data" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    id="My Super Cool Dataset">
  <update insertIfNotExists="false" skipIfError="false">
    <!-- Model Object -->
  </update>
  <insert updateIfExists="false" skipIfError="false">
    <!-- Model Object -->
  </insert>
</dataset>
```

The two options for dataset manipulation are:

* **insert -** Used to perform an insert on the database. Installation of the data is considered "FAILED" if the object already exists or is detected to be a duplicate. The @updateIfExists key is only used if an insertion was attempted and a duplicate primary key was detected. It does not check classifiers.
* **update** - Used to perform a lookup by classifier / key and update the object. If an object does not exist, or a classifier key does not exist and @insertIfNotExists is true, then an insert is done. Typically this operation is safer than insert, but is slower.

The following objects are supported on the dataset:

* Concept
* ConceptClass
* ConceptSet
* ReferenceTerm
* CodeSystem
* Place
* Organization
* Material
* ManufacturedMaterial
* ExtensionType
* IdentifierType
* AssigningAuthority

### Generating a Dataset File

You can generate a dataset from existing data in the SanteDB server by using the SanteDB Administration Console (sdbac) application. To do this you will use the `cdr.query` command, which is illustrated below to produce a dataset of all concepts in the FamilyMember concept set:

```markup
cdr.query -r Concept conceptSet.mnemonic=FamilyMember --dataset > output.dataset
```

You can now easily modify the existing concepts from within the dataset.

{% hint style="info" %}
You can use the user interfaces setup your data and then run the above CDR query to generate a related dataset. This makes your data portable to other SanteDB instances.
{% endhint %}
