# Spring-Boot-Interview-Questions

## How will you configure a DataSource using Spring Boot?

Spring Boot uses an opinionated algorithms to  scan for and configure a DataSource. This allows us to get a fully configured DataSource
implementation by default.
Spring boot configures a lightning fast connection pool like HirakiCP, Apache TomCat or COmmons DBCP depending on those present in class path.
Sometimes we want to configure the DataSource instead of Spring boot doing it for us.