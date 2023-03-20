# SQLALCHEMY



Generating Mappings from multiple Schemas:

The AutomapBase.prepare() method when used with reflection may reflect tables from one schema at a time at most, using the AutomapBase.prepare.schema parameter to indicate the name of a schema to be reflected from. 

In order to populate the AutomapBase with tables from multiple schemas, AutomapBase.prepare() may be invoked multiple times, each time passing a different name to the AutomapBase.prepare.schema parameter. The AutomapBase.prepare() method keeps an internal list of Table objects that have already been mapped, and will add new mappings only for those Table objects that are new since the last time AutomapBase.prepare() was run.


The vast majority of what automap accomplishes is the generation of relationship() structures based on foreign keys. 

The mechanism by which this works for many-to-one and one-to-many relationships is as follows:

1. A given Table, known to be mapped to a particular class, is examined for ForeignKeyConstraint objects.

2. From each ForeignKeyConstraint, the remote Table object present is matched up to the class to which it is to be mapped, if any, else it is skipped.

3. As the ForeignKeyConstraint we are examining corresponds to a reference from the immediate mapped class, the relationship will be set up as a many-to-one referring to the referred class; a corresponding one-to-many backref will be created on the referred class referring to this class.

4. The names of the relationships are determined using the AutomapBase.prepare.name_for_scalar_relationship and AutomapBase.prepare.name_for_collection_relationship callable functions.

5. The classes are inspected for an existing mapped property matching these names. If one is detected on one side, but none on the other side, AutomapBase attempts to create a relationship on the missing side, then uses the relationship.back_populates parameter in order to point the new relationship to the other side.

6. In the usual case where no relationship is on either side, AutomapBase.prepare() produces a relationship() on the “many-to-one” side and matches it to the other using the relationship.backref parameter.



Specifying the classes Explicitly 


The automap extension allows classes to be defined explicitly, in a way similar to that of the DeferredReflection class. 
Classes that extend from AutomapBase act like regular declarative classes, but are not immediately mapped after their construction, and are instead mapped when we call AutomapBase.prepare(). 
The AutomapBase.prepare() method will make use of the classes we’ve established based on the table name we use.

