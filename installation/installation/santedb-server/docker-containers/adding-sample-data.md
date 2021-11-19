# Adding Sample Data

You can quickly add test/sample data by copying [dataset files](../../../../developers/extending-santesuite/extending-santedb/applets/distributing-data.md) into the `/santedb/data` directory of the docker container either using a custom dockerfile or by mounting a volume from the docker image.

## Dataset Files

These dataset files can be generated from the `sdbac` command prompt with the `cdr.query` command to produce dataset files. Dataset files provide a 1:1 mapping to the underlying CDR storage engine and are expressed in XML RIM objects. Dataset files can include:

* Infrastructure elements like Assigning Authorities, Concepts, Extension Types, etc.
* Clinical elements like Entities or Acts&#x20;

For example, to initialize an MPI with an identity domain, and an organization with a custom policy, for a particular use case, create a new dataset file containing the identity domain, organization and custom policy:

```markup
<?xml version="1.0"?>
<dataset id="Elbonia Identity Domains" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <!-- National Health Identifier -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>Elbonia</name>
      <domainName>MOH_NHID</domainName>
      <oid>1.3.6.1.4.1.52820.5.0.1.1.1</oid>
      <url>http://mpi.moh.gov.elb/identity/moh/nhid</url>
      <isUnique>true</isUnique>
      <validation>^\d{12}$</validation>
      <scope>bacd9c6f-3fa9-481e-9636-37457962804d</scope>
    </AssigningAuthority>
  </insert>
  <update insertIfNotExists="true">
    <Organization xmlns="http://santedb.org/model">
      <id>fae7b5fb-ea49-4460-9149-f0952efe572a</id>
      <classConcept>7c08bd55-4d42-49cd-92f8-6388d6c4183f</classConcept>
      <determinerConcept>f29f08de-78a7-4a5e-aeaf-7b545ba19a09</determinerConcept>
      <statusConcept>c8064cbd-fa06-4530-b430-1a52f1530c27</statusConcept>
	    <industryConcept>fdeb2e4e-9e02-4ce3-ab69-cece5ffdee20</industryConcept>
      <name>
        <use>1ec9583a-b019-4baa-b856-b99caf368656</use>
        <component>
          <value>Elbonia National Health Insurnace Corporation</value>
        </component>
      </name>
    </Organization>
  </update>  
  <update insertIfNotExists="true">
    <SecurityPolicy xmlns="http://santedb.org/model">
      <id>fd8c0e00-82fb-11eb-8dcd-0242ac130004</id>
      <name>Elbonia Parlimentarian Health Record VIP Access Policy</name>
      <oid>2.25.40394829382872728372832</oid>
      <isPublic>true</isPublic>
      <canOverride>false</canOverride>
    </SecurityPolicy>
  </update>  
</dataset>
```

The file would be copied into the /santedb/data directory of the santedb-mpi or santedb-icdr container with the following Dockerfile.

```markup
FROM santedb-icdr:latest
COPY custom.dataset /santedb/data/custom.dataset
```

## FHIR Resources

You can also seed data into the `/santedb/data/fhir `directory of the container using a custom dockerfile or by mounting the volume from the docker container.

FHIR resources are limited to only those resources which have a IFhirResourceHandler implementation registered and configured. (TODO: Insert link)

FHIR resources can be in JSON or in XML format, and are simply placed in the directory. The seeder then processes these files on application start and will generate two files:

* A file with a .completed extension which indicates that the message contents were successfully processed and included into the SanteDB iCDR database.
* A file with a .response extension which is the FHIR response that would have been sent via the REST API. This is useful for diagnosing issues with your FHIR message being seeded.

{% hint style="info" %}
Seeding data via FHIR requires at least version 2.1.11 of the iCDR FHIR plugin.
{% endhint %}

## Deploying on Container

You can deploy either dataset files or FHIR files onto your running iCDR container by either including the files in a custom `Dockerfile` such as:

```
FROM santedb-icdr:latest
COPY patients.json /santedb/data/fhir/patients.json
COPY identity.dataset /santedb/data/identity.dataset
```

Alternately , you can mount the `/santedb/data` directory as a volume for your container and copy the files, or you can use a command line interface and `docker cp` such as:

```
docker cp patients.json santedb-icdr:/santedb/data
docker cp identity.dataset santedb-icdr:/santedb/data
```

