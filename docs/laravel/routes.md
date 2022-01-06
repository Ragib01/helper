```
$router->group(['middleware' => ['authUser','auth:api']], function () use ($router) {

    $router->group(['prefix' => 'event-user'],function() use ($router){
        $router->get('/all', 'EventUserController@index');
        $router->post('/create', 'EventUserController@store');
        $router->put('/update', 'EventUserController@update');
        $router->delete('/{id}', 'EventUserController@destroy');
    });

});
```