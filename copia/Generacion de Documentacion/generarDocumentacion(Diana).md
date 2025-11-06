# Documentación con Sphinx

El proceso de generar documentación con **Sphinx** puede resultar algo tedioso al principio, especialmente si es la primera vez que se utiliza. A continuación, se describen los pasos seguidos para configurar y generar la documentación de un proyecto en Python.

---

### 1. Instalación de Python y pip

Para trabajar con Sphinx es necesario tener **Python** y **pip** instalados.
En mi caso, ya tenía Python, por lo que únicamente fue necesario instalar pip con los siguientes comandos:

```bash
python -m ensurepip --default-pip
python -m pip --version
```

---

### 2. Instalación de Sphinx

Una vez configurado pip, instalamos Sphinx junto con algunos complementos útiles:

```bash
python -m pip install sphinx sphinx-autodoc-typehints
```

---

### 3. Creación del proyecto

Sphinx incluye un asistente para crear la estructura inicial del proyecto. Para ello se ejecuta:

```bash
sphinx-quickstart
```

Este comando genera una carpeta con los archivos básicos y solicita información como el nombre del proyecto, autor, etc.

Para comprobar que Sphinx se ha instalado correctamente, se puede utilizar:

```bash
python -m pip show sphinx
```

---

### 4. Configuración del `conf.py`

Dentro de la carpeta **source** se encuentra el archivo `conf.py`, que requiere algunas modificaciones.
En primer lugar, añadimos la ruta del proyecto para que Sphinx pueda acceder a nuestros módulos:

```python
import os
import sys
sys.path.insert(0, os.path.abspath('../src'))  # Ajustar según la ubicación del archivo .py
```

Posteriormente, se activan las extensiones necesarias:

```python
extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.napoleon',     # Permite el uso de docstrings estilo Google/Numpy
    'sphinx_autodoc_typehints',
]
```

---

### 5. Configuración del `index.rst`

El archivo principal `index.rst` define la estructura de la documentación. Un ejemplo básico sería:

```rst
Prueba documentation
====================

Bienvenido a la documentación de Prueba.

Índice
------

.. toctree::
   :maxdepth: 2
   :caption: Contenido:

   python_api
```

---

### 6. Archivo `python_api.rst`

Este archivo genera la documentación de un módulo de Python mediante autodoc. En este caso:

```rst
API de Python
=============

.. automodule:: conversor   # Aquí se coloca el nombre del archivo .py
   :members:
```

---

### 7. Generación de la documentación

Finalmente, se genera la documentación en formato HTML.

* En **Linux**:

  ```bash
  make html
  ```

* En **Windows**:

  ```bash
  make.bat html
  ```

El resultado se encuentra en la carpeta `build/html`, donde se puede abrir el archivo `index.html` para visualizar la documentación.

------

# Documentación con JSDoc

En el caso de JavaScript, la generación de documentación resulta más sencilla gracias a **JSDoc**. A continuación, se detallan los pasos seguidos:

---

### 1. Instalación de JSDoc

JSDoc se puede instalar de dos formas: **global** o **local**.

* Instalación global (recomendada si se quiere usar en varios proyectos):

```bash
npm install -g jsdoc
```

* Instalación local en el proyecto:

```bash
npm install --save-dev jsdoc
```

En este caso, la instalación local no funcionó correctamente, por lo que se optó por la versión global.

---

### 2. Generación de la documentación

Una vez instalado, la documentación se genera con el comando:

```bash
jsdoc <archivo_o_carpeta> -d <carpeta_destino>
```

Por ejemplo, para documentar el archivo `conversor.js` y guardar la salida en la carpeta `docs/js/`:

```bash
jsdoc src/conversor.js -d docs/js/
```

---

### 3. Resultado

La documentación se genera automáticamente en formato HTML en la carpeta indicada (`docs/js/` en este caso). El proceso es rápido, directo y no requiere configuraciones adicionales.

---

# Documentación con PHPDocumentor

Para la documentación de proyectos en **PHP** se utiliza **phpDocumentor**. El procedimiento seguido fue el siguiente:

---

### 1. Instalación de phpDocumentor

En primer lugar, fue necesario descargar el archivo `phpDocumentor.phar` mediante **curl**, ya que no se contaba con Composer previamente instalado:

```bash
curl -L -o phpDocumentor.phar https://github.com/phpDocumentor/phpDocumentor/releases/latest/download/phpDocumentor.phar
```

---

### 2. Configuración inicial

Después de descargarlo, se le otorgan permisos de ejecución:

```bash
chmod +x phpDocumentor.phar
```

Para comprobar la instalación se puede verificar la versión:

```bash
php phpDocumentor.phar --version
```

Opcionalmente, se puede renombrar el archivo para simplificar el uso:

```bash
mv phpDocumentor.phar phpdoc.phar
```

---

### 3. Generación de la documentación

La forma correcta de generar la documentación es:

```bash
php ./phpdoc.phar -d <directorio_fuente> -t <directorio_salida>
```

Ejemplo:

```bash
php ./phpdoc.phar -d src/ -t docs/php/
```

Esto analiza los archivos PHP contenidos en `src/` y genera la documentación en formato HTML dentro de la carpeta `docs/php/`.
