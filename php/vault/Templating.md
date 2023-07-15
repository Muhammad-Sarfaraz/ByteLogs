# Templating 


```php
class TemplateEngine {
    protected $data = [];

    public function setData($key, $value) {
        $this->data[$key] = $value;
    }

    public function render($templateFile) {
        $content = file_get_contents($templateFile);
        foreach ($this->data as $key => $value) {
            $content = str_replace("{{ $key }}", $value, $content);
        }
        return $content;
    }
}

// Usage
$template = new TemplateEngine();
$template->setData('name', 'John Doe');
$template->setData('age', 25);

$html = $template->render('template.html');
echo $html;
```
