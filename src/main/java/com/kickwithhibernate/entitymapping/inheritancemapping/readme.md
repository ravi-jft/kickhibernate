# Hibernate supports 3 types of Inheritance Mappings:
        Table per class hierarchy.
        Table per sub-class hierarchy.
        Table per concrete class hierarchy.

# @Inheritance:
Defines the inheritance strategy to be used for an entity class hierarchy.
        It is specified on the entity class that is the root of the entity class hierarchy.
        If the Inheritance annotation is not specified or if no inheritance type is specified for an entity class hierarchy,
        the SINGLE_TABLE mapping strategy is used.
