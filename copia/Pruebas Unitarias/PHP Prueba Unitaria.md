# Pruebas unitarias PHP


## Estructura del proyecto al final

```
Proyecto1/
├── php
│   ├── src/
|   │   └── saludo.php        # Código principal
|   ├── tests/
|   │   └── SaludoTest.php    # Pruebas unitarias
|   ├── vendor/               # Dependencias de Composer (PHPUnit)
|   ├── composer.json
|   ├── composer.lock
└── .gitignore               # Ignora archivos               
```
`.gitignore` recomendado:

```
vendor/
*.log
*.cache
```

---

## Código principal (`src/saludo.php`)

```php
<?php
/**
 * Devuelve un saludo personalizado.
 *
 * @param string $nombre Nombre del usuario
 *
 * @return string Mensaje de saludo
 */
function saludar(string $nombre): string
{
    return "Hola, " . $nombre . "!";
}

// Ejemplo de uso
echo saludar("Cristina");
?>
```

---

## Instalación de PHPUnit

1. Instalar Composer si no está disponible: [https://getcomposer.org/](https://getcomposer.org/)

```bash
composer require --dev phpunit/phpunit ^10
```

2. Verificar instalación:

```bash
php vendor/bin/phpunit --version
```

---

## Pruebas unitarias (`tests/SaludoTest.php`)

```php
<?php
use PHPUnit\Framework\TestCase;

// Incluir el archivo con la función a testear
require_once __DIR__ . '/../src/saludo.php';

class SaludoTest extends TestCase
{
    public function testSaludarNombreBasico()
    {
        $this->assertEquals("Hola, Cristina!", saludar("Cristina"));
        $this->assertEquals("Hola, Juan!", saludar("Juan"));
        $this->assertEquals("Hola, María!", saludar("María"));
    }

    /**
     * @dataProvider nombresProvider
     */
    public function testSaludarParametrizado($nombre, $esperado)
    {
        $this->assertEquals($esperado, saludar($nombre));
    }

    public function nombresProvider()
    {
        return [
            ["Pedro", "Hola, Pedro!"],
            ["Ana", "Hola, Ana!"],
            ["Luis", "Hola, Luis!"]
        ];
    }
}
```

---

## Ejecutar pruebas

Desde php/:

```bash
php vendor/bin/phpunit --colors=always tests/SaludoTest.php
```

**Resultado:**

```
Hola, Cristina!
PHPUnit 10.5.58 by Sebastian Bergmann and contributors.

D...                                                                4
/ 4 (100%)

Time: 00:00.015, Memory: 8.00 MB

OK, but there were issues!
Tests: 4, Assertions: 5, PHPUnit Deprecations: 1.
```

---

## Errores encontrados y soluciones

### Error 1: `No such file or directory` al ejecutar PHPUnit

**Síntomas:**

```bash
bash: vendor/bin/phpunit: No such file or directory
```

**Causa:** PHPUnit no estaba instalado.

**Solución:**

```bash
composer require --dev phpunit/phpunit ^10
```

Luego ejecutar:

```bash
php vendor/bin/phpunit --colors=always tests/SaludoTest.php
```

---

### Error 2: `Class test_saludo cannot be found`

**Síntomas:**

```
Class test_saludo cannot be found in tests/test_saludo.php
```

**Causa:** El archivo y la clase no seguían la convención de PHPUnit (`*Test.php` y clase `*Test`).

**Solución:**

1. Renombrar el archivo:

```
tests/test_saludo.php  -->  tests/SaludoTest.php
```

2. Renombrar la clase dentro del archivo:

```php
class SaludoTest extends TestCase
```

---

## Flujo de trabajo

1. Crear o cambiar a la rama `release/PHP`:

```bash
git checkout -b release/PHP   # Si no existe
git checkout release/PHP      # Si ya existe
```

2. Traer archivos específicos desde `develop`:

```bash
git checkout develop -- saludo.php
```

3. Mis commits:

```bash
git commit -m "Estructura basica"
git commit -m "Creacion test"
git commit -m "Instalacion PHPUnit"
git commit -m "Corregir estructura"
git commit -m "Contenido test_saludo.php"
git commit -m "Corregido ubicacion vendor"
git commit -m "Corrigiendo error"
git commit -m "Corrigiendo error.2"
git commit -m "Errores solucionados"
git commit -m "Archivos que quiero ignorar"
```

1. Ejecutar PHPUnit para verificar:

```bash
php vendor/bin/phpunit --colors=always tests/SaludoTest.php
```

5. Fusionar a `main`:

```bash
git checkout main

git merge release/PHP
```
---
