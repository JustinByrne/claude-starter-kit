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

## Parameters
- When a function or method has more than one parameter, put each parameter on its own line, with a trailing comma after the last one.
- A single parameter can stay on the same line as the declaration.

```php
// Do
public function send(
    User $user,
    string $message,
): void {
    // ...
}

public function find(int $id): ?User
{
    // ...
}

// Don't
public function send(User $user, string $message): void
{
    // ...
}
```

## Empty functions
- Put the braces of an empty function or method body on their own lines, with a `//` comment inside. This includes constructors that only use property promotion.

```php
// Do
public function __construct(
    public Service $service,
) {
    //
}

// Don't
public function __construct(public Service $service) {}
```
