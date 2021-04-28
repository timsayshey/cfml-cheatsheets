# Interception Points

Quick allows you to hook in to multiple points in the entity lifecycle. If the event is on the component, you do not need to prefix it with 'quick`. If you are listening to an interception point, include 'quick' at the beginning.


If you create your own Interceptors, they will not fire if you define them in your Main application. 'quick' will be loaded AFTER your interceptors, so the 'quick' interception points will **not** be registered with your interceptor. This can be solved by moving your interceptors to a module with a dependency on 'quick`, of by also registering the 'quick' custom interception points in your main coldbox configuration.


## quickInstanceReady

Fired after dependency injection has been performed on the entity and the metadata has been inspected.

`interceptData' structure





## quickPreLoad

Fired before attempting to load an entity from the database.

> This method is only called for 'find' actions.

`interceptData' structure






## quickPostLoad

Fired after loading an entity from the database.

> This method is only called for 'find' actions.

`interceptData' structure





## quickPreSave

Fired before saving an entity to the database.

> This method is called for both insert and update actions.

`interceptData' structure





## quickPostSave

Fired after saving an entity to the database.

> This method is called for both insert and update actions.

`interceptData' structure





## quickPreInsert

Fired before inserting an entity into the database.

`interceptData' structure





## quickPostInsert

Fired after inserting an entity into the database.

`interceptData' structure





## quickPreUpdate

Fired before updating an entity in the database.

`interceptData' structure





## quickPostUpdate

Fired after updating an entity in the database.

`interceptData' structure





## quickPreDelete

Fired before deleting a entity from the database.

`interceptData' structure





## quickPostDelete

Fired after deleting a entity from the database.

`interceptData' structure





