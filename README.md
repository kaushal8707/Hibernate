# Hibernate

Hibernate

Youtube Video Link  :  ----->  https://www.youtube.com/watch?v=JR7-EdxDSf0&t=8929s


21:30   add hibernate and sql dependency in maven projcet
31:30   to make normal class as an Entity  class
35:30   auto creating table in DB
36:30   table created and successfully run with hibernate application
37:50   Service Registry
40:00   auto create table option update / create difference(always better to use update)
41:40   show_sql property
43:25   Annotations(@Entity, @Table, @Id, @Column, @Transient(to ignore data to store into DB) )
48:15   How to fetch data
50:55   get()

52:35   How to use Embeddable Object(58:45) (@Embeddable)(@Entity create new table but it contain table data into another table)

1:00:35  Mapping Relations Theory(@OneToOne(ll create lapid column into Student table, @OneToMany, @ManyToOne, ManyToMany)
		 (1 Student 1 Laptop, 1 Student Many Laptops, Many Laptops belongs to 1 Student, Many Students having Many Laptop and  vice-versa.... )
		@OneToOne(ll create lapid column into Student table)
		(@OneToMany by default create one new table with lid and sid, but if we don't need to create a 3rd table we just need Laptop table having the Student id for that create Student object into Laptop Entity with @ManyToOne annotation and restrict Studententity to create extra table by adding mappedBy Parameter into @OneToMany annotation example @OneToMany(mappedBy="stu") stu is the object ref inside the Laptop Entity class......)
		(@ManyToMany by default create one new table with lid and sid, but if we don't need to create a 3rd table we just need Student table having the Laptop id for that create List<Student> object into Laptop Entity and List<Laptop> object into Student table with @ManyToMany annotation and restrict Student entity to create extra table by adding mappedBy Parameter into @ManyToMany annotation example @ManyToMany(mappedBy="stu") stu is the object ref inside the Laptop Entity class......)
		
1:29:05 Fetch EAGER LAZY
		@OneToMany(mappedBy="laptop",fetch=FetchType.EAGER) By Default FetchType is LAZY
		If any Entity having some dependency so that object would not be loaded till its needed in case of Lazy if Eager then both will be loaded....like If Student class having Laptop object for any relationship....
		
1:35:35  Hibernate Caching (If want to access the same data multiple times so instead of hitting the db all the times can 		access from the cache...
		(first level cache scope to same session object but second level cache scope to different session also but fot same application or sessionfactory object, By Default Second Level Cache is Desabled )
		For multiple sessions if we want to shared some data we should go for the Second Level Cache
		- In pom.xml add ehcache and hibernate-ehcache(Integration) dependency for maven repository 
		- In hibernate.cfg.xml file add the ehcache service provider name
		(<property name="hibernate.cache.use_second_level_cache">true</property>)
		(<property name="hibernate.cache.region.factory_class">hibernate.cache.ehcache.EhCacheRegionfactory</property>)
		
		- We need to change our Entity Bcz by default not all the Entity is Cacheable, so add 2 annotations, @Cacheable and @Cache(usage=CacheConcurrencyStrategy.READONLY) 

1:44:10 Hibernate 1 Level Cache

1:50:10 Hibernate 2 Level Cache

2:00:10 Hibernate Level 2 Caching with Query( HQL)
         If we use second level cache then it enable by default for get() method not for Query....so for Query we need to add one more property in hibernate.cfg.xml file..... and in query setCacheable(true);
		 <property name="hibernate.cache.use_query_cache">true</property>
		 
         Query q1=session.createQuery("from Alien where aid=101");
		 q1.setCacheable(true);
		 Alien a=q1.uniqueResult();

2:05:00  HQL ( Hibernate Query Language(HQL)Theory

		- Query q=session.createQuery("from Student");
		List<Student> students=
		q.list();
		
		-Query q=session.createQuery("from Student where marks > 50");
		
		-Query q=session.createQuery("from Student where rollno=7");
		Student student=q.uniqueResult();
		
		-Query q=session.createQuery("select rollno,name,marks from Student where rollno=7");
		Object[] student=(Object[])q.uniqueResult();
		
		-Query q=session.createQuery("select rollno,name,marks from Student");
		List<Object[]> students=(List<Object[]>)q.list();

		-Query q=session.createQuery("select sum(marks) from Student s where s.marks>60");
		long marks=(Long)q.uniqueResult();

2:27:00 SQL Query ( Native Query )
        SQLQuery query=session.createSQLQuery("select * from student where marks>60");
		query.addEntity(Student.class);
		List<Student> students=query.list(); 

2:34:05  Hibernate Object States / Persistence Life Cycle
		Transient :- First all the newly created objects are in transient state.When we create object in Hibernate it ll be in Transient.if u did any changes with the object and then destroy the object u ll not get the  data back bcz that data was not in persistent state mean not stored in db. By default all the objects are Transient. 
		Persistent:- If u want the data  back then make sure that u obj should be in persistent state. In hibernate if u want to save or persiste the data then u should either use save()/persist() data. the moment u used the method save() and persist() with session object then the object moves into persistent state.
		     Now In persistent state whatever u ll be do with the object it will be there into the database. so there is direct linkage with ur obj with the database row. 
		     after save the object using session if u are modifing the object or change the object still it will applicable to change will happened into db as well. bcz we have not remove the object from the persistent state. 
		Detached:- if the obj is in persistent state and u modifingsomething everytime when u modify it will effect to db aswell and u don't want to do that. may be u want to perform some operation and that operationu don't wantto do into the DB. sobefore that u make sure either u commit ur session or u close ur session or u have to detach the obj from session or persistent state. 
		so we can use method like detach().
		
2:47:45  Get Vs Load
        Main difference in case of performance and exception throws
		Everytime when u use get() it will hit the db and give the object but load() will always give the proxy object. proxy obj is not an actual object. get ll give the object but load will not give the object it only give the object when u use that object. rarely we used load always we used get().
		      if we don't have an obj in db which we trying to access through get() it will give null or null pointer exception but when we use load() we got ObjectNotFoundException.

2:53:00   JPA
			  
		      
		     
		





