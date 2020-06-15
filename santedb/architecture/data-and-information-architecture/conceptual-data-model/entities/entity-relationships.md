# Entity Relationships

Figure 2 represents a sample information model of a kit of BCG vaccine. The model illustrates how a single tuples in the SanteDB model are related to one another to represent a kit. The material “BCG Vaccine” is comprised of one dose of “BCG Antigen”, one “Syringe”, and one dose of “BCG Diluent”. A box of “BCG Vaccine” represents 25 single doses of “BCG Vaccine” \(meaning 25 syringes, 25 antigen and 25 diluent\). Finally, from this we can order \(via instantiation or inheriting a kind\) a kit of GSK 5ml BCG vaccine. This derivation will have the same rules applied \(in that this vaccine must have a syringe, antigen, and diluent.

![Figure 2 - Kitting of BCG](../../../../../.gitbook/assets/image%20%2859%29.png)

Figure 3 represents a complex scenario of kitting a vaccine and then deriving a specific type of kit. The relationship between the instantiation and the generic concepts of the material would have a type of “Manufactured” meaning the “GSK 5 ml BCG” is a manufactured representation of the generic BCGvaccine.

![Figure 3 - Instantiating BCG Vaccine kit to Manufactured Materials ](../../../../../.gitbook/assets/image%20%281%29.png)

The SanteDB model also supports more simplistic representation of a “BCG Vaccine” if kits are not required by the jurisdiction that is implementing SanteDB. Figure 4 illustrates a valid representation of BCG in a jurisdiction where only the antigen is tracked.

![Figure 4 - Representing an instance of a KIND of Entity](../../../../../.gitbook/assets/image%20%2853%29.png)

### 

