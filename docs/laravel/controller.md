## Module
```
namespace App\Http\Controllers\Module;

use App\Models\Module\Model;
use Illuminate\Http\Request;
use App\Http\Controllers\Controller;
```

## Index
```
public function index()
{
    $var = Slider::customPaginate();
    return response()->json($var);
}  
```

## Store
```
public  function  store(Request  $request)

{
    $var  =  new  Model;

    $var->title  =  $request['title'];
    $var->created_by  =  config()->get('global.user_id');

    if($var->save()){

        return  response()->json([

        'message'  =>  'New var added successfully',

        'data'  =>  $var

    ],201);

    }

}
```

## Update
```
public  function  update(Request  $request)

{
    $var  =  Model::find($request['id']);

    $var->title  =  $request['title'];
    $var->updated_by  =  config()->get('global.user_id');

    if($var->update()){

        return  response()->json([

        'message'  =>  'Successfully updated',

        'data'  =>  $var

        ],201);

        }else{

        return  response()->json([

        'message'  =>  'Something went wrong!'

        ], 400);

    }

}
```

## Delete
```
public function destroy(int $id, Model $model)
{
    $del = Model::find($id);
    if($del){
        $del->delete();
        return response()->json(['message' =>'successfully deleted ..'],200);
    }else{
        return response()->json(['message' => '.. to be deleted not found'],404);
    }
}
```