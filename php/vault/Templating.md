# Templating 
A template is a predefined structure that serves as a blueprint for generating consistent and reusable content, separating presentation from logic and allowing for dynamic data insertion.

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
