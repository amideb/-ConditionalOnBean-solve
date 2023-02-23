If you have two classes implementing CommandLineRunner, and you want to use only one of them in your Spring Boot application, you can use the @Primary annotation on the bean that you want to use, just like we did in the previous answer.

Here's an example:

```sh
@Configuration
public class AppConfig {
    @Bean
    @Primary
    public MyFirstCommandLineRunner myFirstCommandLineRunner() {
        return new MyFirstCommandLineRunner();
    }

    @Bean
    public MySecondCommandLineRunner mySecondCommandLineRunner() {
        return new MySecondCommandLineRunner();
    }
}
```

In this example, we have two classes that implement CommandLineRunner: MyFirstCommandLineRunner and MySecondCommandLineRunner. We want to use MyFirstCommandLineRunner in our Spring Boot application, so we've annotated the myFirstCommandLineRunner() method with @Primary.

Now, when we run our Spring Boot application, Spring will use the myFirstCommandLineRunner() method to create the bean, since it is annotated with @Primary.

Here's an example of how you can use @ConditionalOnBean to conditionally create a bean based on the presence of another bean:

```
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }

    @Bean
    @ConditionalOnBean(MyService.class)
    public MyCommandLineRunner myCommandLineRunner() {
        return new MyCommandLineRunner();
    }
}
```

In this example, we have a MyService bean and a MyCommandLineRunner bean. We only want to create the MyCommandLineRunner bean if the MyService bean is present.

We've annotated the myCommandLineRunner() method with @ConditionalOnBean(MyService.class). This means that Spring will only create the myCommandLineRunner() bean if the MyService bean is already present in the application context.

If the MyService bean is not present, the myCommandLineRunner() bean will not be created.
