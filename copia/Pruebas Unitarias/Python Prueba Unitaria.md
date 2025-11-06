# Pruebas unitarias Python

## Estructura del proyecto al final

```
Proyecto1/
├── python/
│   ├── .pytest_cache/      # Guarda información de las pruebas
│   ├── .venv/               # Entorno virtual local
│   ├── src/
│   │   ├── __init__.py      # Para tratar la carpeta como paquete
│   │   └── parOimpar.py     # Función principal
│   └── tests/
│       └── test_parOimpar.py # Pruebas unitarias
└── .gitignore               # Ignora archivos
```

`.gitignore`:

```
.venv/
__pycache__/
*.pyc
.pytest_cache/

```

---

## Código principal (`src/parOimpar.py`)

```python
"""
Módulo para verificar si un número es par o impar.
"""

def es_par(numero):
    """
    Verifica si un número es par.

    Args:
        numero (int): Número a evaluar.

    Returns:
        bool: True si el número es par, False si es impar.
    """
    if not isinstance(numero, int):
        raise TypeError("El valor debe ser un número entero")
    return numero % 2 == 0


if __name__ == "__main__":
    # Ejemplos de uso
    print("¿4 es par?", es_par(4))  # True
    print("¿7 es par?", es_par(7))  # False
```

Traigo el archivo desde develop con el siguiente comando:

```bash
git checkout develop -- parOimpar.py

```
---

## Creación del entorno virtual y pytest

1. Crear entorno virtual dentro de `python/`:

```bash
python -m venv .venv
```

2. Activar entorno virtual (Git Bash en Windows):

```bash
source .venv/Scripts/activate
```

3. Instalar `pytest`:

```bash
pip install pytest
```

4. Verificar instalación:

```bash
pytest --version
```

---

## Pruebas unitarias (`tests/test_parOimpar.py`)

```python
import sys
import os

# Agregar carpeta src al path para que pytest encuentre el módulo
sys.path.insert(0, os.path.abspath(os.path.join(os.path.dirname(__file__), '..', 'src')))

from parOimpar import es_par
import pytest

def test_es_par_casos_basicos():
    assert es_par(4) is True
    assert es_par(0) is True
    assert es_par(7) is False
    assert es_par(-3) is False

@pytest.mark.parametrize("value,expected", [
    (2, True),
    (3, False),
    (10, True),
    (-2, True),
    (1, False),
])
def test_parametrizado(value, expected):
    assert es_par(value) == expected

def test_tipo_invalido():
    with pytest.raises(TypeError):
        es_par("hola")
```

---

## Errores encontrados y soluciones

### Error 1: `pytest` no encontrado

**Síntomas:**

```
bash: pytest: command not found
```

**Solución:**

1. Activar entorno virtual correctamente en Git Bash:

```bash
source .venv/Scripts/activate
```

2. Instalar `pytest`:

```bash
pip install pytest
```

---

### Error 2: `ModuleNotFoundError: No module named 'src'`

**Síntomas:**

```
from src.parOimpar import es_par
ModuleNotFoundError: No module named 'src'
```

**Causas:**

* Carpeta se llamaba `src_py` en vez de `src`.
* Python no encuentra la carpeta `src` como paquete.

**Solución:**

1. Renombrar carpeta:

```bash
mv src_py src
```

2. Crear `__init__.py` dentro de `src`:

```bash
touch src/__init__.py
```

3. Ajustar imports en el test (si es necesario):

```python
from src.parOimpar import es_par
```

**Alternativa en Windows/Git Bash:** agregar `src` al `sys.path` al inicio del test (como en el código final).

---

## Ejecución de tests

Activar entorno virtual:

```bash
source .venv/Scripts/activate
```

Ejecutar pytest desde la carpeta `python/`:

```bash
pytest
```

**Resultado:**

```
collected 7 items

tests/test_parOimpar.py ....... [100%]
7 passed
```

---

## Flujo de trabajo

1. Crear rama `release/Python`:

```bash
git checkout -b release/Python
```

2. Traer archivos específicos desde `develop`:

```bash
git checkout develop -- parOimpar.py
```

3. Mis commits:

```bash
git commit -m "Base test Python"
git commit -m "Contenido test_parOimpar.py"
git commit -m "Organización y entorno virtual"
git commit -m "Primer error"
git commit -m "Intento solucion error"
git commit -m "Segundo error"
git commit -m "Intento solucion error2"
git commit -m "Intento solucion error2.2"
git commit -m "Errores solucionados"
git commit -m "Archivos que quiero ignorar"
git commit -m "Archivos que quiero ignorar2"
```

1. Ejecutar pytest para verificar que todo pasa antes de mergear a `main`.

2. Fusionar a `main`:

```bash
git checkout main

git merge release/Python
```
---
