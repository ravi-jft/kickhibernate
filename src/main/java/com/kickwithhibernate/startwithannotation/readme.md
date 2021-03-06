<p> Hibernate Annotations are based on the JPA 2 specification and supports all the features.
        *All the JPA annotations are defined in the javax.persistence.* package.
        *Hibernate EntityManager implements the interfaces and life cycle defined by the JPA specification.
        *The core advantage of using hibernate annotation is that you don't need to create mapping (hbm) file.
        *Here, hibernate annotations are used to provide the meta data.



# @Entity:
<p>package: import javax.persistence.Entity; <br>
        Contents:Which java bean we want to persist in database, add @Entity annotation on it.<p>
<code>
e.g:-
@Entity
public class User {....}
</code>

# @Table:
<p> package: import javax.persistence.Table;<br>
        content: Specifies the primary table for the annotated entity. Additional tables may be specified using SecondaryTable or SecondaryTables annotation.
        If no Table annotation is specified for an entity class, the default values apply. </p><br>
<code>
e.g:
@Entity
@Table(name="CUST", schema="RECORDS")
public class Customer { ... }
</code>


 # @Column:
<p> package: import javax.persistence.Column;
        content: It is used to specify the mapped column for a persistent property or field.</p> <br>
<code>
e.g:
@Column(name = "email_address", nullable = true, length = 120)
private String emailAddress;
</code>

# @Id:
<p>package: import javax.persistence.Id;<br>
        content: Specifies the primary key of an entity. <p><br>
<code>
e.g:-
@Id
private Long id;
</code>

 # @GeneratedValue:
<p> package: import javax.persistence.GeneratedValue;<br>
        content: Provides for the specification of generation strategies for the values of primary keys, default strategy is GenerationType.AUTO. <p> <br>
<code>
e.g:-
@Id
@GeneratedValue
private Long id;
</code>

# @Version:
<p> package: import javax.persistence.Version; <br>
        content: Specifies the version field or property of an entity class that serves as its optimistic lock value.
        The version is used to ensure integrity when performing the merge operation and for optimistic concurrency control. </p> <br>
<code>
e.g:-
@Version
private Long version;
</code>

# @OrderBy:
<p>package: import javax.persistence.OrderBy;<br>
        content: Specifies the ordering of the elements of a collection valued association or element collection at the point when the association or collection is retrieved.<br>
<code>
e.g:-
@OrderBy("createdOn desc")
private List<Book> books;
</code>

# @Transient:
<p> import javax.persistence.Transient;<br>
        content: @Transient annotation is used to indicate that a field is not to be persisted in the database.</p><br>
<code>
e.g:-
@Transient
private String confirmPassword;
</code>

# @Lob:
<p> package: import javax.persistence.Lob; <br>
        content -> @Lob used to specifies that a persistent property or field should be persisted as a large object to a database-supported large object type.<p> <br>
<code>
e.g:1-
@Lob
protected String report;

</code> <br>
<code>
        e.g:2-
@Lob
protected byte[] pic;
</code> <br>

# Hibernate Inheritance Mapping Annotations

# @Inheritance:

<p1>package: import javax.persistence.Inheritance;<br>
        content: Defines the inheritance strategy to be used for an entity class hierarchy.<br>
        It is specified on the entity class that is the root of the entity class hierarchy.<br>
        If the Inheritance annotation is not specified or if no inheritance type is specified for an entity class hierarchy, the SINGLE_TABLE mapping strategy is used.</p> <br>
<code>
e.g:-
@Inheritance(strategy= InheritanceType.JOINED)
public class Employee {}
</code>

# @DiscriminatorColumn:
<p1>package: import javax.persistence.DiscriminatorColumn;<br>
        content:It Is used to define the discriminator column for the SINGLE_TABLE and JOINED inheritance mapping strategies.<br>
        The strategy and the discriminator column are only specified in the root of an entity class hierarchy or subhierarchy in which a different inheritance strategy is applied.<br>
        If the DiscriminatorColumn annotation is missing, and a discriminator column is required, the name of the discriminator column defaults to "DTYPE" and the discriminator type to DiscriminatorType.STRING.</p> <br>

<code>
Example:
@Entity
@Table(name="CUST")
@Inheritance(strategy=SINGLE_TABLE)
@DiscriminatorColumn(name="DISC", discriminatorType=STRING,length=20)
public class Customer { ... }
<br>
@Entity
public class ValuedCustomer extends Customer { ... }
</code>

# @DiscriminatorValue:
<p>package: import javax.persistence.DiscriminatorValue; <br>
        Is used to specify the value of the discriminator column for entities of the given type. <br>
        The DiscriminatorValue annotation can only be specified on a concrete entity class. <br>
        If the DiscriminatorValue annotation is not specified and a discriminator column is used, a provider-specific function will be used to generate a value representing the entity type. If the DiscriminatorType is STRING, the discriminator value default is the entity name.</p> <br>
<code>
Example:

@Entity
@Table(name="CUST")
@Inheritance(strategy=SINGLE_TABLE)
@DiscriminatorColumn(name="DISC", discriminatorType=STRING,length=20)
@DiscriminatorValue("CUSTOMER")
public class Customer { ... }

@Entity
@DiscriminatorValue("VCUSTOMER")
public class ValuedCustomer extends Customer { ... }
</code> <br>

# @PrimaryKeyJoinColumn:
<p> package: import javax.persistence.PrimaryKeyJoinColumn; <br>
        content: This annotation specifies a primary key column that is used as a foreign key to join to another table.
        It is used to join the primary table of an entity subclass in the JOINED mapping strategy to the primary table of its superclass;
        it is used within a SecondaryTable annotation to join a secondary table to a primary table;
        and it may be used in a OneToOne mapping in which the primary key of the referencing entity is used as a foreign key to the referenced entity.
        If no PrimaryKeyJoinColumn annotation is specified for a subclass in the JOINED mapping strategy, the foreign key columns are assumed to have the same names as the primary key columns of the primary table of the superclass </p> <br>

<code>
Example: Customer and ValuedCustomer subclass

@Entity
@Table(name="CUST")
@Inheritance(strategy=JOINED)
@DiscriminatorValue("CUST")
public class Customer { ... }
<br>
@Entity
@Table(name="VCUST")
@DiscriminatorValue("VCUST")
@PrimaryKeyJoinColumn(name="CUST_ID")
public class ValuedCustomer extends Customer { ... }
</code>


# @JoinColumn:
<p>import javax.persistence.JoinColumn; <br>
        content: Specifies a column for joining an entity association or element collection.
        If the JoinColumn annotation itself is defaulted, a single join column is assumed and the default values apply. <br>
<code>
Example:

@ManyToOne
@JoinColumn(name="ADDR_ID")
public Address getAddress() { return address; }
</code>


# @JoinTable:
<p> package: import javax.persistence.JoinTable;<br>
        content : Used in the mapping of associations. It is specified on the owning side of an association.
        A join table is typically used in the mapping of many-to-many and unidirectional one-to-many associations.
        It may also be used to map bidirectional many-to-one/one-to-many associations, unidirectional many-to-one relationships, and one-to-one associations (both bidirectional and unidirectional).
        When a join table is used in mapping a relationship with an embeddable class on the owning side of the relationship, the containing entity rather than the embeddable class is considered the owner of the relationship.
        If the JoinTable annotation is missing, the default values of the annotation elements apply.
        The name of the join table is assumed to be the table names of the associated primary tables concatenated together (owning side first) using an underscore.<br>
<code>
Example:
<br>
@JoinTable(
        name="CUST_PHONE",
        joinColumns=
        @JoinColumn(name="CUST_ID", referencedColumnName="ID"),
        inverseJoinColumns=
        @JoinColumn(name="PHONE_ID", referencedColumnName="ID")
)
</code> <br>

# @MapsId:
<p>package: import javax.persistence.MapsId <br>
        content: Designates a ManyToOne or OneToOne relationship attribute that provides the mapping for an EmbeddedId primary key,
        an attribute within an EmbeddedId primary key, or a simple primary key of the parent entity.
        The value element specifies the attribute within a composite key to which the relationship attribute corresponds.
        If the entity's primary key is of the same Java type as the primary key of the entity referenced by the relationship, the value attribute is not specified. <br>

<code>
Example:

// parent entity has simple primary key
<br>
@Entity
public class Employee {
    @Id long empId;
    String name;
    ...
}
<br>
// dependent entity uses EmbeddedId for composite key

@Embeddable
public class DependentId {
    String name;
    long empid;   // corresponds to primary key type of Employee
}
<br>
@Entity
public class Dependent {
    @EmbeddedId DependentId id;
    ...
    @MapsId("empid")  //  maps the empid attribute of embedded id
    @ManyToOne Employee emp;
}
</code> <br>

# Hibernate Association Mapping Annotations

# @OneToOne:
<p> package: import javax.persistence.OneToOne;
        content: This annotation defines a single-valued association to another entity that has one-to-one multiplicity.
        It is not normally necessary to specify the associated target entity explicitly since it can usually be inferred from the type of the object being referenced.

<code>
Example :

@Entity
public class User {
    @OneToOne
    private UserProfile userProfile;
}
</code><br>

# @ManyToOne:
<p>package import javax.persistence.ManyToOne;
        content: Defines a single-valued association to another entity class that has many-to-one multiplicity.
        It is not normally necessary to specify the target entity explicitly since it can usually be inferred from the type of the object being referenced. If the relationship is bidirectional, the non-owning OneToMany entity side must used the mappedBy element to specify the relationship field or property of the entity that is the owner of the relationship.
        The ManyToOne annotation may be used within an embeddable class to specify a relationship from the embeddable class to an entity class.
        If the relationship is bidirectional, the non-owning OneToMany entity side must use the mappedBy element of the OneToMany annotation to specify the relationship field or property of the embeddable field or property on the owning side of the relationship.
        The dot (".") notation syntax must be used in the mappedBy element to indicate the relationship attribute within the embedded attribute. The value of each identifier used with the dot notation is the name of the respective embedded field or property.
<code>
Example:
<br>
@ManyToOne(optional=false)
@JoinColumn(name="CUST_ID", nullable=false, updatable=false)
public Customer getCustomer() { return customer; }
</code>
<br>

# @OneToMany:
<p>package: import javax.persistence.OneToMany;<br>
        content:Defines a many-valued association with one-to-many multiplicity. If the collection is defined using generics to specify the element type, the associated target entity type need not be specified; otherwise the target entity class must be specified. If the relationship is bidirectional, the mappedBy element must be used to specify the relationship field or property of the entity that is the owner of the relationship.
        The OneToMany annotation may be used within an embeddable class contained within an entity class to specify a relationship to a collection of entities. If the relationship is bidirectional,
        the mappedBy element must be used to specify the relationship field or property of the entity that is the owner of the relationship.
        When the collection is a java.util.Map, the cascade element and the orphanRemoval element apply to the map value.</p> ,br>
<code>
Example 1: One-to-Many association using generics

// In Customer class:

@OneToMany(cascade=ALL, mappedBy="customer")
public Set<Order> getOrders() { return orders; }
<br>
        In Order class:
<br>
@ManyToOne
@JoinColumn(name="CUST_ID", nullable=false)
public Customer getCustomer() { return customer; }
</code>

# @ManyToMany:
<p>package: import javax.persistence.ManyToMany;<br>
        content: Defines a many-valued association with many-to-many multiplicity.
        Every many-to-many association has two sides, the owning side and the non-owning, or inverse, side. The join table is specified on the owning side. If the association is bidirectional, either side may be designated as the owning side. If the relationship is bidirectional, the non-owning side must use the mappedBy element of the ManyToMany annotation to specify the relationship field or property of the owning side.
        The join table for the relationship, if not defaulted, is specified on the owning side.
        The ManyToMany annotation may be used within an embeddable class contained within an entity class to specify a relationship to a collection of entities. If the relationship is bidirectional and the entity containing the embeddable class is the owner of the relationship, the non-owning side must use the mappedBy element of the ManyToMany annotation to specify the relationship field or property of the embeddable class.
        The dot (".") notation syntax must be used in the mappedBy element to indicate the relationship attribute within the embedded attribute.
        The value of each identifier used with the dot notation is the name of the respective embedded field or property.</p> <br>

<code>
Example 1:

// In Customer class:

@ManyToMany
@JoinTable(name="CUST_PHONES")
public Set<PhoneNumber> getPhones() { return phones; }

// In PhoneNumber class:

@ManyToMany(mappedBy="phones")
public Set<Customer> getCustomers() { return customers; }
</code>
