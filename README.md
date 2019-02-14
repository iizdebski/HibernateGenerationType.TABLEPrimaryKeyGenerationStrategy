# HibernateGenerationType.TABLEPrimaryKeyGenerationStrategy

The generation type TABLE gets only rarely used nowadays. It simulates a sequence by storing and updating its current value in a database table which requires the use of pessimistic locks which put all transactions into a sequential order. This slows down your application, and you should, therefore, prefer the GeneratinType.SEQUENCE, if your database supports sequences, which most popular databases do.

@Id

@Column(name=”employee_id”)

@GeneratedValue(strategy=GenerationType.TABLE)

Private Integer employeeId;

You can use the @TableGenerator annotation in a similar way as the already explained @SequenceGenerator annotation to specify the database table which Hibernate shall use to simulate the sequence.

@Id

@Column(name=”employee_id”)

@GeneratedValue(strategy=GenerationType.TABLE,generator=”empid_generator”)

@TableGenerator(name=”empid_generator”, table=”empid_generator”, schema=”hibernatedb”)

JPA offers 4 different ways to generate primary key values:

AUTO: Hibernate selects the generation strategy based on the used dialect;

IDENTITY: Hibernate relies on an auto_incremented database column to generate the primary key;

SEQUENCE: Hibernate requests the primary key value from a database sequence.

TABLE: Hibernate uses a database table to simulate a sequence.

We should prefer to use the GenerationTypeSEQUENCE because it is very efficient and allows Hibernate to decide when to perform the insert statement. This provides the required flexibility to use other performance optimization techniques like JDBC batching.
