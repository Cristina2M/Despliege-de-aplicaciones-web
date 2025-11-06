# Ejercicio Git, pruebas unitarias y documentación (+cherry pick)

## 1. Estructura del repositorio

```
reloj/
│
├── src/
│   ├── ver1.html
│   ├── ver2.html
│   └── reloj.js
│
├── tests/
│   └── reloj.test.js
│
├── README.md
└── package.json
```

---

## 2. Inicializar el repositorio

```bash
# Creo el repositorio y añado los archivos base
git init

# Añado los archivos iniciales
git add .
git commit -m "Archivos base"

# Crear y cambiar a develop
git checkout -b develop
```

---

## 3. Crear ramas feature (dos versiones distintas)

Creamos dos ramas para las dos versiones del ejercicio:

```bash
# Rama para la versión que usa padStart en el js
git checkout -b feature/V-padstart
# Copiar ver1.html a src/
git add src/ver1.html
git commit -m "Versión 1"

# Volvemos a develop y creamos la otra feature
git checkout develop
git checkout -b feature/V-helper
# Copiar ver2.html a src/
git add src/ver2.html
git commit -m "Versión 2"
```

---

## 4. Refactor: extraer lógica JS a `src/reloj.js` (preparación para tests)

Creo un archivo común `src/reloj.js` para poder testear:

**`src/reloj.js`**

```js
export const formatearTiempo = (unidad) => unidad < 10 ? '0' + unidad : String(unidad);

export const obtenerHoraFormateada = (date = new Date()) => {
  return `${formatearTiempo(date.getHours())}:${formatearTiempo(date.getMinutes())}:${formatearTiempo(date.getSeconds())}`;
};
```

Ejemplo de commit en cada rama:

```bash
# En feature/V-padstart
git add src/reloj.js
git commit -m "rsrc/reloj.js (padStart/Vers1)"

# En feature/V-helper
git add src/reloj.js
git commit -m "src/reloj.js (formatearTiempo helper/Vers2)"
```

---

## 5. Forzar un conflicto de merge (modificar misma línea)

Para provocar conflictos con propósito, edito la misma línea en ambas ramas. 

```js
// En feature/V-padstart (Vers1)
console.log(`Son las ${horas}h y ${minutos}m`);

// En feature/V-helper (Vers2)
console.log(`Hora y minutos formateados: ${horas}h y ${minutos}m`);
```

Ahora intento fusionar ambos features en `develop`:

```bash
# Estando en develop
git checkout develop

git merge feature/V-padstart
# merge ok

git merge feature/V-helper
# Aquí aparecerá un conflicto
```

### Mensaje de conflicto

Git muestra algo parecido a:

```
Auto-merging src/reloj.js
CONFLICT (content): Merge conflict in src/reloj.js
Automatic merge failed; fix conflicts and then commit the result.
```

### Cómo resolver el conflicto

1. Abre `src/reloj.js`. Aparecen marcas de conflicto:

```
<<<<<<< HEAD
console.log(`Son las ${horas}h y ${minutos}m`);
=======
console.log(`Hora y minutos formateados: ${horas}h y ${minutos}m`);
>>>>>>> feature/V-helper
```

1. Decido la versión final:

```js
// Solución
console.log(`Son las ${horas}h y ${minutos}m — Hora y minutos formateados`);
```

3. Guardar, `git add` y `git commit`:

```bash
git add src/reloj.js
git commit -m "Resolver conflicto en src/reloj.js"
```

> Si decido cancelar la fusión:
>
> ```bash
> git merge --abort
> ```

---

## 6. Rebase: reescribir la historia para limpiar commits

El `rebase` se usa para poner una rama encima de otra actualizada. Por ejemplo: rebasar `feature/V-helper` sobre `feature/V-padstart` para aplicar los cambios de padstart antes de la otra branch.

```bash
# Me sitúo en la rama que quiero reescribir
git checkout feature/V-helper
# Rebase interactivo sobre la rama objetivo
git rebase feature/V-padstart
```

### Rebase interactivo (squash/editar commits)

```bash
git rebase -i HEAD~3
# Se abrire el editor para escoger pick/squash/reword
```

Pueden aparecer conflictos durante el rebase y Git detendrá el proceso. Se resuelven con un `git add` y con:

```bash
git rebase --continue
```

Para cancelar:

```bash
git rebase --abort
```

---

## 7. Cherry-pick: copiar commits específicos entre ramas

En `feature/V-helper` he hecho un commit con un arreglo que quiero aplicar a `feature/V-padstart`.

1. Obtener el hash del commit (por ejemplo `abc1234`):

```bash
git log --oneline
```

1. Lo aplico en la otra rama:

```bash
git checkout feature/v-padstart
git cherry-pick abc1234
```

Si hay conflictos durante el cherry-pick, los resuelvo y luego:

```bash
git add <fichero>
git cherry-pick --continue
```

Para cancelar:

```bash
git cherry-pick --abort
```

---

## 9. Pruebas unitarias con Jest

### Inicializar NPM y instalar Jest (si aún no lo tenías)

```bash
npm init -y
npm install --save-dev jest
```

Añade en `package.json`:

```json
{
  "scripts": {
    "test": "jest"
  }
}
```

### Test

**`tests/reloj.test.js`**

```js
import { formatearTiempo, obtenerHoraFormateada } from '../src/reloj.js';

test('añade cero delante de números menores que 10', () => {
  expect(formatearTiempo(5)).toBe('05');
});

test('no añade cero si el número es mayor o igual que 10', () => {
  expect(formatearTiempo(12)).toBe('12');
});

// Test con fecha controlada
test('obtenerHoraFormateada con Date fijo', () => {
  const date = new Date('2020-01-02T03:04:05');
  expect(obtenerHoraFormateada(date)).toBe('03:04:05');
});
```

Ejecutar tests:

```bash
npm test
```

---



