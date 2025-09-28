# Documentación de Código: Python, JavaScript y PHP


| Aspecto / Lenguaje       | **Python** | **JavaScript (JSDoc)** | **PHP (PHPDoc)** |
|--------------------------|------------|-----------------------|-----------------|
| **Cómo documentar**       | Usando **docstrings** (`"""..."""`) al inicio de funciones, clases y módulos. | Usando comentarios **JSDoc** (`/** ... */`) antes de funciones, clases y métodos. | Usando comentarios **PHPDoc** (`/** ... */`) antes de funciones, clases, métodos y propiedades. |
| **Parámetros**            | Describir nombre, tipo y propósito con `Args:`. | Describir nombre, tipo y propósito con `@param {tipo} nombre - descripción`. | Describir nombre, tipo y propósito con `@param tipo $nombre Descripción`. |
| **Valor de retorno**      | Explicar tipo y significado con `Returns:`. | Explicar tipo y significado con `@returns {tipo} descripción`. | Explicar tipo y significado con `@return tipo Descripción`. |
| **Errores / Excepciones** | Documentar con `Raises:` indicando qué excepciones puede lanzar. | Usar `@throws {ErrorType}` si la función puede lanzar errores. | Usar `@throws TipoError` para errores que puede lanzar la función. |
| **Ejemplos**              | Incluir ejemplo bajo `Example:` o en docstring. | Incluir con `@example` mostrando uso real de la función. | Incluir con `@example` mostrando cómo llamar la función o método. |
| **Buenas prácticas**      | - Documentar funciones, clases y módulos.<br>- Explicar propósito, parámetros, retorno y excepciones.<br>- Mantener docstrings actualizados.<br>- No explicar línea a línea, explicar **qué hace**. | - Documentar todas las funciones y métodos públicos.<br>- Usar `@param`, `@returns` y `@example`.<br>- Añadir `@deprecated` si se deja de usar.<br>- Mantener coherencia de estilo JSDoc. | - Documentar funciones, métodos y propiedades públicas.<br>- Explicar parámetros, retorno y posibles errores.<br>- Incluir ejemplos claros.<br>- Mantener documentación sincronizada con cambios del código. |
| **Control de versiones**  | Gestionar cambios con Git u otra herramienta.<br>Commits frecuentes y descriptivos.<br>Etiquetar versiones importantes con `tags`. | Igual que Python, mantener historial de cambios y versiones. | Igual que Python, usar Git para registrar cambios y versiones. |
| **Estructura sugerida de repositorio** | ```/python\nejercicios/\nREADME.md``` | ```/javascript\nejercicios/\nREADME.md``` | ```/php\nejercicios/\nREADME.md``` |
