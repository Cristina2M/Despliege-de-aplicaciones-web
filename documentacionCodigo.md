# Documentación de Código: Python, JavaScript y PHP


| Aspecto / Lenguaje       | **Python** | **JavaScript (JSDoc)** | **PHP (PHPDoc)** |
|--------------------------|------------|-----------------------|-----------------|
| **Cómo documentar**       | Usando **docstrings** (`"""..."""`) al inicio de funciones, clases y módulos. | Usando comentarios **JSDoc** (`/** ... */`) antes de funciones, clases y métodos. |
| **Parámetros**            | Describir nombre, tipo y propósito con `Args:`. | Describir nombre, tipo y propósito con `@param {tipo} nombre - descripción`. |
| **Valor de retorno**      | Explicar tipo y significado con `Returns:`. | Explicar tipo y significado con `@returns {tipo} descripción`. |
| **Errores / Excepciones** | Documentar con `Raises:` indicando qué excepciones puede lanzar. | Usar `@throws {ErrorType}` si la función puede lanzar errores. |
| **Ejemplos**              | Incluir ejemplo bajo `Example:` o en docstring. | Incluir con `@example` mostrando uso real de la función. |
| **Buenas prácticas**      | - Documentar funciones, clases y módulos.<br>- Explicar propósito, parámetros, retorno y excepciones.<br>- Mantener docstrings actualizados.<br>- No explicar línea a línea, explicar **qué hace**. | - Documentar todas las funciones y métodos públicos.<br>- Usar `@param`, `@returns` y `@example`.<br>- Añadir `@deprecated` si se deja de usar.<br>- Mantener coherencia de estilo JSDoc. |
| **Control de versiones**  | Gestionar cambios con Git u otra herramienta.<br>Commits frecuentes y descriptivos.<br>Etiquetar versiones importantes con `tags`. | Igual que Python, mantener historial de cambios y versiones. | 
| **Estructura sugerida de repositorio** | ```/python\nejercicios/\nREADME.md``` | ```/javascript\nejercicios/\nREADME.md``` |
