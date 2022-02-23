# Establishing Minimum Datasets

## Resources

The SanteDB team has provided a template which lists all the data elements captured in SanteDB for Patients, Places, Organizations, and Persons.&#x20;

{% file src="../../../../.gitbook/assets/SanteMPI Minimum Dataset Worksheet.xlsx" %}

To complete this worksheet:

1. Review the readme for the meaning of each column and type of data which should be present.
2. For each data element in the provided SanteDB information model, review:
   1. The commonality of the data element in your context (how often is it captured? is it useful information to be captured? If asked, would a patient know the information? etc.)
   2. Relevant legislation in the context (is it illegal to capture? if not are there any protections which need to be in place?)
   3. The sensitivity of the information (if we ask patients for this information will they lie? will they offer the information?)
   4. Mapping to local semantics (is the data known as a different name? is there a mapping of semantics?). For example, many implementing jurisdictions may need to map the address hierarchy to match their country context, or some countries may not use family names, etc.&#x20;
3. Document the context specific use of each field.

Once complete, the information on this worksheet will make its way into formal specifications (such as IHE ITI TF Volume 4 content, FHIR implementation guides, etc.). This process is not covered on the community wiki.

### Demoland Example Dataset Worksheet

The SanteDB team has provided a completed worksheet which illustrates the minimum dataset and mappings for Demoland. Changes from the template are highlighted in green.

{% file src="../../../../.gitbook/assets/SanteMPI Minimum Dataset Worksheet - Demoland.xlsx" %}
