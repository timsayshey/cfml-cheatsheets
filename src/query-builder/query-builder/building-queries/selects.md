# Selects

## select

If you pass no columns to this method, it will default to "*".

```javascript
.select( [ "fname AS firstName", "age" ] ).from( "users" )
```
## distinct

Calling distinct will cause the query to be executed with the DISTINCT keyword.

```javascript
.select( "username" ).distinct().from( "users" )
```
## addSelect

This method adds the columns passed to it to the currently selected columns.

```javascript
.addSelect( [ "fname AS firstName", "age" ] ).from( "users" )
```

## selectRaw

A shortcut to use a raw expression in the select clause.

```javascript
.selectRaw( "YEAR(birthdate) AS birth_year" ).from( "users" )
```

## subSelect

The subselect is added to the other already selected columns.

```javascript
.subSelect( "last_login_date", ( q ) => {
  q.selectRaw( "MAX(created_date)" ).from( "logins" )
} ) ).from( "users" )
```

## clearSelect

Clears out the selected columns for a query along with any configured select bindings.

```javascript
.from( "users" )
    .select( [ "fname AS firstName", "age" ] )
    .clearSelect()
```
## reselect

Clears out the selected columns for a query along with any configured select bindings.

```javascript
.from( "users" )
    .select( [ "fname AS firstName", "age" ] )
    .reselect( "username" )
```
## reselectRaw

Clears out the selected columns.

```javascript
.from( "users" ).select( [ "fname AS firstName", "age" ] )
    .reselectRaw( "YEAR(birthdate) AS birth_year" )
```