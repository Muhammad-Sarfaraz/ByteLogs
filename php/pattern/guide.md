# Guide
- Builder
- Singleton
- Strategic
- Facade

## Builder

```SMSBuilder.php```
```php
<?php

namespace App\Builder;

class SMSBuilder
{
    protected $message;

    protected $to;

    public function message($message)
    {
        $this->message = $message;

        return $this;
    }

    public function to($to)
    {
        $this->to = $to;

        return $this;
    }

    public function send()
    {
        $smsRequest = send_sms($this->to,$this->message)
    }

}
```

```Execute.php```
```php
echo (new SMSBuilder())->to('xxxx-xxx-xx')->message('All Ok!');
```
