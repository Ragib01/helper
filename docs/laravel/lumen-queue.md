## SendEmail.php
```
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;

class SendEmail extends Mailable
{
    use Queueable, SerializesModels;

    public $subject, $short_name, $body;
    public function __construct($subject, $short_name, $body)
    {
        $this->subject = $subject;
        $this->short_name = $short_name;
        $this->body = $body;
    }

    
    public function build()
    {
        return $this->from(env('COMPANY_NOREPLY_ACCOUNT'), $this->short_name)
        ->subject($this->subject)
        ->view('mail.main', ['html' => $this->body]);
    }
}
```

## SendMailJob.php
```
<?php

namespace App\Jobs;
use Illuminate\Support\Facades\Log;
use Illuminate\Support\Facades\Mail;
use App\Mail\SendEmail;

class SendMailJob extends Job
{
    
    protected $to, $subject, $short_name, $body;


    public function __construct($subject, $short_name, $to, $body)
    {
        $this->subject = $subject;
        $this->short_name = $short_name;
        $this->body = $body;
        $this->to = $to;
    }

  
    public function handle()
    {
        $email = new SendEmail($this->subject, $this->short_name, $this->body);        
        Mail::to($this->to)->send($email);
    }
}
```


## Controller
```
$data = [
	'subject' => 'Invitation from Company_name',
	'short_name' => 'Company_name',
	'body' => 'You are invited from Company_name for joining '.$batch->course_alias_name_en.' For join click the link </br>'.$link,
	'to'   => $email_or_phone,
	'link' => $link,
	'message' => 'You are invited from Company_name for joining '.$batch->course_alias_name_en.' For join click the link '.$link
];

if(is_numeric($email_or_phone)){
	dispatch(new SendSmsJob($data['to'], $data['message']));
}else{
	dispatch(new SendMailJob($data['subject'], $data['short_name'], $data['to'], $data['body']));
}
```