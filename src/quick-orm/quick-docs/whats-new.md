# What's New?

## 4.2.0

* Add a ['simplePaginate'](guide-1/getting-started/retrieving-entities.md#simplepaginate) pagination method for quicker performance when total records or total pages are not needed or too slow.

## 4.1.6

* Configure columns are no longer cleared when setting up a 'BelongsToMany' relationship.

## 4.1.5

* Provide 'initialThroughConstraints' for 'hasOne' relationships \(used in '*Through' relationships\).

## 4.1.4

* Ignore orders when retrieving a relationship count.

## 4.1.1, 4.1.2

* Preserve casted value after saving an entity.

## 4.1.0

* Allow for [child entities,](guide-1/getting-started/defining-an-entity/subclass-entities.md) including [discriminated entities.](guide-1/getting-started/defining-an-entity/subclass-entities.md#discriminated-entities)
* Look up returning values by column name not by alias in the 'ReturningKeyType`.

## 4.0.2

* Skip eager loading database call when no keys are found.
* Only apply 'CONCAT' when needed in '*Through' relationships.

## 4.0.1

* Use 'WHERE EXISTS' over 'DISTINCT' when fetching relationships.  'DISTINCT' restricts some of the queries that can be run.

## 4.0.0


📹  [Watch a walkthrough of these changes on CFCasts.](https://cfcasts.com/series/whats-new-in-quick-4)


#### BREAKING CHANGES

* [Scopes](guide-1/getting-started/query-scopes-and-subselects.md), ['whereHas'](guide-1/relationships/querying-relationships.md#wherehas), and ['whereDoesntHave'](guide-1/relationships/querying-relationships.md#wheredoesnthave) callbacks now automatically group where clauses when an 'OR' combinator is detected.

#### Other Changes

* Dynamically add [relationship counts](guide-1/relationships/relationship-counts.md) to a parent entity without loading all of the relationship.
* Give a helpful error message when trying to set relationship values before saving an entity, where applicable.
* Multiple bug fixes related to [subselects](guide-1/getting-started/query-scopes-and-subselects.md#subselects) and [querying relationships ](guide-1/relationships/querying-relationships.md)when using 'belongsToThrough`, 'hasOneThrough`, or 'hasManyThrough`.

## 3.1.7

* Correct jQuery link in test runner.

## 3.1.6

* Allow expressions in basic where clauses.
* Fix 'delete' naming collision.

## 3.1.5

* Add an alias to 'with' to QuickBuilder.

## 3.1.4

* Fix a stack overflow on nested relationship checks.

## 3.1.3

* Configured tables \('.from'\) are now used for qualifying columns.

## 3.1.2

* Remove unnecessary nesting in compare queries.

## 3.1.1

* Fix [querying relationship methods](guide-1/relationships/querying-relationships.md) when using "OR" combinators.

## 3.1.0

* Add support for JSON [casting](guide-1/getting-started/defining-an-entity/#casts) using a new 'JsonCast@quick' component.

## 3.0.4

* Compatibility updates for ColdBox 6

## 3.0.3

* Optimize [cast ](guide-1/getting-started/defining-an-entity/#casts)caching

## 3.0.2

* Apply [custom sqltypes ](guide-1/getting-started/defining-an-entity/#sql-type)during [eager loading](guide-1/relationships/eager-loading.md).

## 3.0.1

* Account for null values in ['fill'](guide-1/getting-started/creating-new-entities.md#fill).
* Swap structAppend order for a Lucee bug in mementifier integration.

## 3.0.0

#### **BREAKING CHANGES** <a id="breaking-changes"></a>

_Please see the_ [_Upgrade Guide_](upgrade-guide.md#3-0-0) _for more information on these changes._

* Drop support for Lucee 4.5 and Adobe ColdFusion 11.
* Virtual Inheritance \(using a 'quick' annotation instead of extending 'quick.models.BaseEntity'\) has been removed.  It was hardly used, and removing it allows us to simplify some of the code paths.
* 'accessors="true"' is now required on every entity.  This is similar to above where requiring it allows us to simplify the codebase immensely.  A helpful error message will be thrown if 'accessors="true"' is not present on your entity.
* The 'defaultGrammar' mapping needs to be the full WireBox mapping, including the '@qb`, if needed.
  * For instance, 'MSSQLGrammar' would become 'MSSQLGrammar@qb`.
  * This will allow for other grammars to be more easily contributed via third party modules.
* \'\`['HasManyThrough' relationships](guide-1/relationships/relationship-types/hasmanythrough.md) now only accept a 'relationships' parameter of relationship methods to walk to get to the intended entity.
* Attributes using 'casts="boolean"' need to be updated to ['casts="BooleanCast@quick"'](guide-1/getting-started/defining-an-entity/#casts).
* Some method and parameter names have been changed to support composite keys.  **The majority of changes will only affect you if you have extended base Quick components.** The full list can be found in the Upgrade Guide.

####  **Other Changes** <a id="other-changes"></a>

* [Bundle Mementifier](guide-1/serialization.md) for memento transformations.
* Use [asMemento](guide-1/serialization.md#asmemento) to automatically convert queries to mementos.
* Automatically-generated [API docs](https://apidocs.ortussolutions.com/#/coldbox-modules/quick/).
* Add error message for defaulting key values.
* Update to [qb 7.0.0](https://qb.ortusbooks.com/).
* Add a [belongsToThrough relationship](guide-1/relationships/relationship-types/belongstothrough.md).
* Add a [HasOneThrough relationship](guide-1/relationships/relationship-types/hasonethrough.md).
* [Custom Casts](guide-1/getting-started/defining-an-entity/#casts) - using custom components to represent one or more attributes.
* [Ordering by relationship attributes](guide-1/relationships/ordering-by-relationships.md).
* [addSubselect](guide-1/getting-started/query-scopes-and-subselects.md#subselects) [improvements](guide-1/getting-started/query-scopes-and-subselects.md#using-relationships-in-subselects).
* Add a new QuickBuilder to better handle interop with qb.
* [Add 'exists' and 'existsOrFail' methods](guide-1/getting-started/retrieving-entities.md#existsorfail).
* Allow [custom](guide-1/getting-started/retrieving-entities.md#existsorfail) [error](guide-1/getting-started/retrieving-entities.md#firstorfail) [messages](guide-1/getting-started/retrieving-entities.md#findorfail) for 'orFail' methods.
* Ensure 'loadRelationship' doesn't reload existing relationships.
* Add multiple retrieve or new/create methods - ['firstWhere'](guide-1/getting-started/retrieving-entities.md#firstwhere), ['firstOrNew'](guide-1/getting-started/retrieving-entities.md#firstornew), ['firstOrCreate'](guide-1/getting-started/retrieving-entities.md#firstorcreate), ['findOrNew'](guide-1/getting-started/retrieving-entities.md#findornew), and ['findOrCreate'](guide-1/getting-started/retrieving-entities.md#findorcreate).
* Add ['paginate'](guide-1/getting-started/retrieving-entities.md#paginate) to Quick.
* Add ['is' and 'isNot'](guide-1/getting-started/defining-an-entity/#comparing-entities) to compare entities.
* Allow [hydrating entities](guide-1/getting-started/retrieving-entities.md#hydrate) from serialized data.
* Allow returning default entities for null relations on ['HasOne'](guide-1/relationships/relationship-types/hasone.md#withdefault), ['BelongsTo'](guide-1/relationships/relationship-types/belongsto.md#withdefault), ['HasOneThrough'](guide-1/relationships/relationship-types/hasonethrough.md#withdefault), and ['BelongsToThrough'](guide-1/relationships/relationship-types/belongstothrough.md#withdefault) relationships.
* Query relations using ['has'](guide-1/relationships/querying-relationships.md#has), ['doesntHave'](guide-1/relationships/querying-relationships.md#doesnthave), ['whereHas'](guide-1/relationships/querying-relationships.md#wherehas), and ['whereDoesntHave'](guide-1/relationships/querying-relationships.md#wheredoesnthave).
* Split 'reset' into 'reset' and 'resetToNew' methods.
* Store the original attributes for later resetting.
* Use 'parameterLimits' to eager load.
* Use a new entity each time on BaseService.
* Apply sql types for columns to 'wheres`.
* Apply global scopes more consistently
* Correctly ignore key column when updating.
* Fix 'hasRelationship' method to only return true for exact matches.
* Better handling of constrained relationships when eager loading.
* Convert aliases when qualifying columns.
* Add a better error message if 'onMissingMethod' fails.
* Only retrieve columns for defined attributes.
* Cache entity metadata in CacheBox.
* Use attribute hash for checking 'isDirty`.

## 2.5.0

* Define [custom collections](guide-1/collections.md) per entity.

## 2.4.0

* ~~Apply custom setters when hydrating from the database.~~ \(Reverted in '2.5.3' for unintended consequences with things like password hashing.\)
* [Query scopes can return any value.](guide-1/getting-started/query-scopes-and-subselects.md#scopes-that-return-values)  This allows you to use scopes to perform query functions and return values.  \(If you do not want to return a custom value, return the 'QueryBuilder' instance or nothing.\)
* Improve error messages for not loaded entities.
* Return the correct memento with accessors on.

## 2.3.0

* [Option to ignore non-existent attributes](guide-1/getting-started/updating-existing-entities.md#update)

## 2.2.0

* [Relationship Fetch Methods](guide-1/relationships/retrieving-relationships.md) \('first' and 'find' methods\)

## 2.1.0

* [Subselect Helper](guide-1/getting-started/query-scopes-and-subselects.md#subselects)
* [Global Scopes](guide-1/getting-started/query-scopes-and-subselects.md#global-scopes)
* [saveMany](guide-1/relationships/relationship-types/hasmany.md#saveMany)
* Mapping foreign keys for relationships is now optional
* Either entities or primary key values can be passed to relationship persistance methods
* Relationships can also be saved by calling '"set" & relationshipName`
* [Virtual Inheritance](guide-1/getting-started/defining-an-entity/) works on ColdBox 5.2+

