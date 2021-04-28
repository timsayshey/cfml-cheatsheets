# Beans scopes










# Customizing a bean

## Initialization method
```Java
@PostConstruct
```

## Destroy method
```Java
@PreDestroy
```

# SpEL : Spring Expression Language

## Access a system properties
```Java
@Value("#{ systemProperties['user.home'] }")
private String defaultHome;
```

## Access a bean property

```Java
@Value("#{myBean.myValue}")
private String myValue;
```

## Parse a string

```Java
@Value("#{myBean.myValue.substring(0,1)}")
private String myValue;
```

## Operations

```Java
@Value("#{myBean.myValue.length() > 2}")
private String myValue;
```
