---
paths:
  - "**/*.php"
---

# PHP

## Formatting
- If the project has a formatter config (e.g. Pint's `pint.json` or PHP-CS-Fixer's `.php-cs-fixer.php`) that sets a different style, follow the config instead of these rules.
- Run the project's formatter on any PHP files you change.

## Arrays
- Always write non-empty arrays across multiple lines, one item per line, even when there is only one item. This includes associative and nested arrays.
- Add a trailing comma after the last item.
- Leave empty arrays inline as `[]`.

```php
// Do
$roles = [
    'admin',
];

$options = [
    'timeout' => 30,
    'retries' => 3,
];

// Don't
$roles = ['admin'];
$options = ['timeout' => 30, 'retries' => 3];
```
