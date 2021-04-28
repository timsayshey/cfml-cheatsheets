var user = getInstance( "User" )
    .where( "active", 1 )
    .whereActive( 1 ); // dynamic
    .whereBetween( "id", 1, 2 );
    .whereColumn( "products.id", "orders.id" );
    .whereExists( existsQuery );
    .whereIn( "id", [ 1, 4, 66 ] );
    .whereLike( "username", "J%" );
    .whereNotNull( "publishedDate" )
    .whereNull( "id" );
    .orWhere( "email", "LIKE", q & "%" );
----------------------------------
    .orderByDesc( "username" )
    .orderBy( "modified_date", "desc" );
    .orderByRaw( "CASE WHEN status = ? THEN 1 ELSE 0 END DESC", [ 1 ] );
    .orderByActive() // dynamic
----------------------------------
    .take( 5 );
    .offset( 25 );
    .limit( 10 )
    .asMemento()
    .asTransient()
    .select( "name", "email", "createdDate" );
    .addSelect( [ "fname AS firstName", "age" ] ).from( "users" );
    .selectRaw( "YEAR(birthdate) AS birth_year" ).from( "users" );
----------------------------------
    .all();
    .existsOrFail( rc.userID );
    .existsOrFail( rc.userID );
    .find( rc.userID );
    .findOrCreate( rc.id, { "name" : "nada" });
    .findOrFail( rc.userID );
    .findOrNew( rc.id, { "name" : "nada" });
    .first();
    .firstOrCreate( { "username": rc.username } );
    .firstOrFail();
    .firstOrNew( { "username": rc.username } );
    .firstWhere( "username", rc.username );
    .forPage( 3, 15 );
    .get();
    .getMemento();
    .paginate( rc.page, rc.maxrows );
    .simplePaginate( rc.page, rc.maxrows );
    .toList( chr( 10 ) );
    .toSQL( showBindings = true ) );
----
    .updateAll();
    .update();
    .save();
    .deleteAll( [ 4, 10, 22 ] );
----------------------------------
Hydration
    .hydrate({ "id": 4, "name": "JaneDoe" }); r.isLoaded(); // true
    .hydrateAll([{ "id": 4, "name": "JaneDoe" },{ "id": 5, "name": "BobDoe" }]);