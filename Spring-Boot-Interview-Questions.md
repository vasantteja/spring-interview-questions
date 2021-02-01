# Spring-Boot-Interview-Questions

### How will you configure a DataSource using Spring Boot?

Spring Boot uses an opinionated algorithms to  scan for and configure a DataSource. This allows us to get a fully configured DataSource
implementation by default.
Spring boot configures a lightning fast connection pool like HirakiCP, Apache TomCat or COmmons DBCP depending on those present in class path.
Sometimes we want to configure the DataSource instead of Spring boot doing it for us.

### How can you configure a DataSource programatically in Spring Boot?

Instead of Spring Boot we can programatically configure DataSource. We need to implement our DataSource implementation in @Configuration class by
creating a bean using @Bean annotation.

```
@Bean
public DataSource getDataSource(){
	DataSourceBuilder dataSourceBuilder = DataSourceBuilder.create();
	dataSourceBuilder.driverClassName("org.h2.Driver");
	dataSourceBuilder.url("jdbc:h2:mem:test);
	dataSourceBuilder.username("SA");
	dataSourceBuilder.password(" ");
	return dataSourceBuilder.build();
}
}
```
8002330268
### How can you configure a DataSource programatically in Spring Boot?

We can create a configuration using Spring Data JPA. Let's analyze this prgramatically.

1. We will create the required entities for all the objects that reside in the respective database.
2. We will configure the repositories for entities which we write to the database.
3. We will write the configuration using JPA. We will have separate configurations for different entities which reside in different databases/datasources.
==> In each of these configuration class we will define following interfaces: -
1. DataSource 2. EntityManagerFactory 3. TransactionManager 
4. In the configuration class we need to mention which TransactionManager you want to be primary using @Primary annotation.
5. The annotations used are: -
@Configuration
@PropertySource({"classpath:persistence-multiple-db-boot.properties"})
@EnableJpaRepositories(
  basePackages = "com.baeldung.multipledb.dao.user",
  entityManagerFactoryRef = "userEntityManager",
  transactionManagerRef = "userTransactionManager")
 6. The interesting part is annotating the data source bean creation method with @ConfigurationProperties. We just need to specify the corresponding config prefix. 
 Inside this method, we're using a DataSourceBuilder, and Spring Boot will automatically take care of the rest. 
 ####How do the configured properties get injected into the DataSource configuration?
 When calling the build() method on the DataSourceBuilder, it'll call its private bind() method:
 
 ```
 public T build() {
    Class<? extends DataSource> type = getType();
    DataSource result = BeanUtils.instantiateClass(type);
    maybeGetDriverClassName();
    bind(result);
    return (T) result;
}
```

This private method performs much of the autoconfiguration magic, binding the resolved configuration to the actual DataSource instance:

```
private void bind(DataSource result) {
    ConfigurationPropertySource source = new MapConfigurationPropertySource(this.properties);
    ConfigurationPropertyNameAliases aliases = new ConfigurationPropertyNameAliases();
    aliases.addAliases("url", "jdbc-url");
    aliases.addAliases("username", "user");
    Binder binder = new Binder(source.withAliases(aliases));
    binder.bind(ConfigurationPropertyName.EMPTY, Bindable.ofInstance(result));
}
```

In Summary here are the steps: -

1. Data source bean definition
2. Entities
3. Entity Manager Factory bean definition
4. Transaction Management
5. Spring Data JPA Repository custom settings  

References:

https://springframework.guru/how-to-configure-multiple-data-sources-in-a-spring-boot-application/

https://www.baeldung.com/spring-data-jpa-multiple-databases

### How do you configure multiple properties files in Spring Boot?

@PropertySource 


 
 