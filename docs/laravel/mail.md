## bcc

```
$emails = ['myoneemail@esomething.com', 'myother@esomething.com','myother2@esomething.com'];

Mail::send('emails.welcome', [], function($message) use ($emails)
{    
    $message->to($emails)->subject('This is test e-mail');    
});
var_dump( Mail:: failures());
exit;
```