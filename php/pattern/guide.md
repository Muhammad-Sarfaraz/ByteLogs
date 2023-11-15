# Guide
- Builder
- Singleton
- Strategic
- Facade
- Transfomer

## Transfomer
Basically a transformer is simple design pattern which is used to transfer a object or data in differents format. That's all, In laravel it is called Resources.
```php
<?php

interface Transformer
{
    public function transform(array $data);
}

class UserTransformer implements Transformer
{
    public function transform(array $data)
    {
        return [
            'id' => $data['id'],
            'username' => $data['username'],
            'email' => $data['email'],
            // Additional fields can be added based on your needs
        ];
    }
}
```

## Builder
The builder pattern is a design pattern designed to provide a flexible solution to various object creation problems in object-oriented programming.

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
