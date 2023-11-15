# Clinical Decision-Support

{% hint style="info" %}
SanteDB 3.0 includes support for a new, more robust Clinical Decision Support system. This page documents the new CDSS subsystem. For documentation on SanteDB 2.x CDSS please see the [Legacy CDSS ](../../../applets/cdss-protocols/legacy-cdss.md)topic.
{% endhint %}

## Introduction

This tutorial is intended to assist developers in getting started with the SanteDB Protocol Definition XML format, the format in which SanteDB clinical protocol rules are expressed.

### What is a Clinical Protocol?

In SanteDB, a clinical protocol is defined as a series of actions that must occur to care for a patient based on a series of entry criteria or rules. SanteDB care planning engine will take one or more protocols for a patient to generate a proposed plan of care for that patient.

Each clinical protocol is defined as a separate series of clinical events that must occur, you don't have to worry about bundling them together. For example, if you are writing a series of clinical protocol rules for DTaP and ROTA you could (and should) seperate out the domains of that protocol.

### How does SanteDB use these protocols?

Whenever a function calls the CarePlanning service, the SanteDB back end will contact the clinical protocol repository to gather a list of IClinicalProtocol implementations to be executed (the XML protocol handler is one of these implementations, but there are others). The care planner then executes the logic in the clinical protocol files asynchronously collecting the results in a CarePlan instance.

If the caller requested that the care planner create proposed encounters (appointments) then the care planner will group the proposed actions in the CarePlan as a periodic hull function of the StartTime - Coalesce(StopTime, ActTime).

### Understanding MoodConcepts

Before we begin writing our clinical protocols, we first have to understand an often overlooked attribute on all SanteDB objects, the MoodConcept. The MoodConcept is described in more detail in the schema and technical documentation, however it will be summarized here for brevity.

All Acts in SanteDB carry with them a mood concept, this instructs data consumers the mode of the data. The most common mood concept are:

| Mood concept   | Description                                                                                |
| -------------- | ------------------------------------------------------------------------------------------ |
| EventOccurence | Indicates that the act **did** occur, meaning something was actually done to the patient.  |
| Intent         | Indicates that the act is something that someone **intends** to do in the future           |
| Request        | Indicates that the act is something that a human is **requesting** be done at a later time |
| Propose        | Indicates that the act is something that is being **proposed** to be completed             |

For the care planner and clinical protocols, we look to the Propose mood concept, as the computer and our protocols are simply proposed steps in a care plan.

### Setting up your Materials or other required assets

Please note that SanteDB does not treat a vaccination protocol differently than any other clinical protocol. This means that if you ware setting up a clinical protocol which relies on materials, places, or other entities, you must ensure that those entities are created appropriately. This can be done using the user interface, or alternately using a dataset file.

## Key Topics

