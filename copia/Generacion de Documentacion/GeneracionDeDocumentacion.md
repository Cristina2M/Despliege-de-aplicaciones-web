
# Documentación del Proyecto

Este proyecto integra diferentes **generadores automáticos de documentación** para **Python, JavaScript y PHP**, siguiendo las herramientas recomendadas. Toda la documentación se genera **localmente** y se organiza en la carpeta `docs/`, lista para ser publicada en un futuro (por ejemplo, en GitHub Pages o buckets).  

---

# Documentación con Sphinx (Python)

### 1. Instalación de Sphinx y extensiones

```bash
pip install sphinx sphinx-autodoc-typehints sphinx_rtd_theme
```

---

### 2. Inicialización del proyecto de documentación

En la carpeta `docs/`:

```bash
sphinx-quickstart
```

Este comando crea la estructura inicial: `source/`, `build/`, `conf.py`, `Makefile` y `make.bat`.

---

### 3. Configuración del `conf.py`

Se activan las extensiones necesarias para autodoc y napoleon:

```python
extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.napoleon',
    'sphinx_autodoc_typehints',
]
```

---

### 4. Generación de la documentación

```bash
cd docs
make html   # o .\make.bat html en Windows
```

La salida se encuentra en `docs/build/html/index.html`.

---

# Documentación con JSDoc (JavaScript)

### 1. Instalación de JSDoc

Dentro del proyecto:

```bash
npm init -y
npm install --save-dev jsdoc
```

---

### 2. Uso de comentarios JSDoc en el código

Ejemplo en `src_js/app.js`:

```javascript
/**
 * Suma dos números.
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function suma(a, b) {
    return a + b;
}
```

---

### 3. Generación de la documentación

```bash
npx jsdoc src_js -d docs/js
```

La salida se encuentra en `docs/js/index.html`.

---

# Documentación con phpDocumentor (PHP)

### 1. Descarga del archivo PHAR

Se utiliza el archivo **`phpDocumentor.phar`** descargado desde GitHub(https://github.com/phpDocumentor/phpDocumentor/releases):

```bash
php phpDocumentor.phar --version
```

---

### 2. Código fuente PHP

Se coloca dentro de la carpeta `php_src/`. Ejemplo de clase:

```php
<?php
/**
 * Clase de utilidades matemáticas
 */
class Matematicas {
    /**
     * Suma dos números
     * @param int $a
     * @param int $b
     * @return int
     */
    public function sumar($a, $b) {
        return $a + $b;
    }
}
```

---

### 3. Generación de la documentación

```bash
php phpDocumentor.phar -d php_src -t docs/php
```

La salida se encuentra en `docs/php/index.html`.


