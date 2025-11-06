# Pruebas unitarias JavaScript


## Estructura del proyecto al final

```
Proyecto1/
└── javascript/
|   ├── src/
|   │   └── alCuadrado.js      # Código principal
|   ├── tests/
|   │   └── alCuadrado.test.js # Pruebas unitarias
|   ├── package.json
|   └── node_modules/
└── .gitignore               # Ignora archivos
```

`.gitignore` recomendado:

```
node_modules/
```

---

## Código principal (`src/alCuadrado.js`)

```js
/**
 * Calcula el cuadrado de un número.
 *
 * @param {number} x - Número a elevar al cuadrado
 * @returns {number} El cuadrado de x
 */
function cuadrado(x) {
  if (typeof x !== 'number') throw new TypeError('Debe ser un número');
  return x * x;
}

// Exportar la función para poder testearla
module.exports = { cuadrado };

// Ejemplo de uso
console.log("El cuadrado de 5 es:", cuadrado(5));
console.log("El cuadrado de 10 es:", cuadrado(10));
```

---

## Instalación de Jest

1. Entrar en la carpeta `javascript`:

```bash
cd javascript
```

2. Inicializar npm e instalar Jest:

```bash
npm init -y
npm install --save-dev jest
```

3. Configurar script de test en `package.json`:

```json
"scripts": {
  "test": "jest"
}
```

---

## Pruebas unitarias (`tests/alCuadrado.test.js`)

```js
const { cuadrado } = require('../src/alCuadrado');

describe('Pruebas de la función cuadrado', () => {
  test('Casos básicos', () => {
    expect(cuadrado(2)).toBe(4);
    expect(cuadrado(0)).toBe(0);
    expect(cuadrado(-3)).toBe(9);
  });

  test.each([
    [5, 25],
    [10, 100],
    [-7, 49],
  ])('cuadrado(%i) debe ser %i', (input, expected) => {
    expect(cuadrado(input)).toBe(expected);
  });

  test('Debe lanzar error si no es número', () => {
    expect(() => cuadrado('hola')).toThrow();
  });
});
```

---

## Ejecutar pruebas

Desde la carpeta `javascript/`:

```bash
npm test
```

Salida:

```
 PASS  tests/alCuadrado.test.js
  Pruebas de la función cuadrado
    √ Casos básicos (5 ms)
    √ cuadrado(5) debe ser 25 (2 ms)
    √ cuadrado(10) debe ser 100 (1 ms)
    √ cuadrado(-7) debe ser 49 (1 ms)
    √ Debe lanzar error si no es número (13 ms)

Test Suites: 1 passed, 1 total
Tests:       5 passed, 5 total
Snapshots:   0 total
Time:        8.895 s
Ran all test suites.
```

---


## Flujo de trabajo

1. Crear o cambiar a la rama `release/JS`:

```bash
git checkout -b release/JavaScript   # Si no existe
git checkout release/JavaScript      # Si ya existe
```

2. Traer archivos específicos desde `develop`:

```bash
git checkout develop -- alCuadrado.js
```

3. Mis commits:

```bash
git commit -m "Estructura base e init -y"
git commit -m "Contenido alCuadrado.test.js"
git commit -m "Todo correcto"
git commit -m "Archivos ignorar"
```

4. Ejecutar pruebas:

```bash
npm test
```

5. Fusionar a `main`:

```bash
git checkout main

git merge release/JavaScript
```
