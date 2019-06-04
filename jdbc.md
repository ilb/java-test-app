# Настройка подключения к базе данных
## Настойка jdbc подключения через JNDI

В файл WEB_INF/web.xml добавить  ссылку на JNDI ресурс
```xml
    <resource-ref>
        <description>filedossier</description>
        <res-ref-name>jdbc/filedossier</res-ref-name>
        <res-type>javax.sql.DataSource</res-type>
        <res-auth>Container</res-auth>
        <res-sharing-scope>Shareable</res-sharing-scope>
    </resource-ref>
```

В файл META-INF/context.xml добавить описание ресурса
```xml
  <Resource auth="Container" driverClassName="com.mysql.jdbc.Driver" logAbandoned="true" maxWaitMillis="20000" name="jdbc/filedossier" 
            password="filedossier" removeAbandonedOnBorrow="true" removeAbandonedTimeout="100" type="javax.sql.DataSource"
            url="jdbc:mysql://localhost:3306/filedossier?serverTimezone=Europe/Samara&amp;rewriteBatchedStatements=true"
            username="filedossier" validationQuery="SELECT 1"/>
```

В application.properties прописать ссылку на ресурс
```
spring.datasource.jndi-name=java:comp/env/jdbc/filedossier
```

## Настойка jdbc подключения через appication.properties для тестов
```
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/filedossier?serverTimezone=Europe/Samara&rewriteBatchedStatements=true
spring.datasource.username=filedossier
spring.datasource.password=filedossier
```

## Настройка jdbc зависимостей
Добавить в pom.xml
```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-jdbc</artifactId>
        </dependency>
```