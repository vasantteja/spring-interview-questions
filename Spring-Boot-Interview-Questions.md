# Spring-Boot-Interview-Questions

## How will you configure a DataSource using Spring Boot?

Spring Boot uses an opinionated algorithms to  scan for and configure a DataSource. This allows us to get a fully configured DataSource
implementation by default.
Spring boot configures a lightning fast connection pool like HirakiCP, Apache TomCat or COmmons DBCP depending on those present in class path.
Sometimes we want to configure the DataSource instead of Spring boot doing it for us.

## How can you configure a DataSource programatically in Spring Boot?

Instead of Spring Boot we can programatically configure DataSource. We need to implement our DataSource implementation in @Configuration class by
creating a bean using @Bean annotation.

`
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
`