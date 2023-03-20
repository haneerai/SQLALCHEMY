# SQLALCHEMY
automap implementation


Generating Mappings from multiple Schemas:

The AutomapBase.prepare() method when used with reflection may reflect tables from one schema at a time at most, using the AutomapBase.prepare.schema parameter to indicate the name of a schema to be reflected from. 

In order to populate the AutomapBase with tables from multiple schemas, AutomapBase.prepare() may be invoked multiple times, each time passing a different name to the AutomapBase.prepare.schema parameter. The AutomapBase.prepare() method keeps an internal list of Table objects that have already been mapped, and will add new mappings only for those Table objects that are new since the last time AutomapBase.prepare() was run.
