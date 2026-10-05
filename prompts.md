## Prompt 1

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Necesito la spec viva de cuentas y acceso del ejercicio del módulo 3. En esta pasada no escribas el archivo: primero tienes que entender qué hace el código hoy.

Lee AGENTS.md, CLAUDE.md y, en README.md, la parte de la tarea (formato, las tres reglas y la parte B). Trabaja en spec-viva-ac. No hagas operaciones de Git que escriban, no inicialices OpenSpec y no modifiques código, pruebas, dependencias, configuración ni el harness. Los únicos archivos permitidos son prompts.md y, más adelante, docs/spec-viva/ac.md.

Registra este prompt entero en prompts.md como Prompt 1. Modelo: Sonnet 5.5. Herramienta: Claude Code.

Recorre registro, inicio de sesión, cierre, recuperación de la sesión al recargar y perfil, en la API y en la pantalla. Conclusiones solo a partir del código. La documentación del repo sirve para situarte, no para dar por hecho que algo está implementado. Si una duda está en una dependencia, ábrela en lo que hay instalado.

Ciérrame con cuatro cosas y para:
1. Mapa corto de archivos que importan.
2. Comportamiento observable que ya puedes afirmar.
3. Puntos que seguirían siendo una duda sin ejecutar la aplicación.
4. Plan de redacción con el formato exacto del ejercicio.

No crees todavía docs/spec-viva/ac.md. No redactes la parte B ni inventes cuántos requisitos habré comprobado yo. Espera a que revise el plan.
```

## Prompt 2

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
El plan está bien. Regístralo como Prompt 2 en prompts.md, con el modelo y la herramienta de esta sesión.

Redacta la parte A de docs/spec-viva/ac.md. Si el archivo ya tiene parte A, sustitúyela. La parte B déjala sin rellenar.

Castellano, con las palabras del formato tal cual:
- ## Purpose, una o dos frases de para qué existe esta capability.
- ## Requirements.
- Cada ### Requirement: dice qué SHALL hacer el sistema, de forma que se pueda comprobar.
- Cada requisito lleva al menos un #### Scenario: con - **WHEN** y - **THEN**. La precondición va dentro del WHEN.

Alcance: cuentas y acceso, nada de tareas. Separa la regla de la API y la de la pantalla cuando no coincidan. Un requisito que no puedas sostener con el código o con la dependencia instalada no entra en Requirements; lo dejas en la respuesta como pendiente.

No afirmes en bloque que un token caduca o que no caduca. Si no hay vencimiento escrito, dilo así, y no lo mezcles con lo que pasa al cerrar sesión. En los requisitos no menciones clases, archivos, dónde se guarda el token ni algoritmos. No uses ADDED, MODIFIED ni REMOVED. No corrijas el código.

Mismos límites de antes: sin Git de escritura y sin OpenSpec. Al terminar, di cuántos requisitos escribiste y proponme tres para abrirlos yo. El archivo y el fragmento van en el chat, fuera de la spec.
```

## Prompt 3

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Se acabó el tiempo de la parte A. No la modifiques y no sigas buscando en el código.

Añade este prompt a prompts.md como Prompt 3. Modelo: Sonnet 5.5. Herramienta: Claude Code.

Debajo de la spec, en docs/spec-viva/ac.md, escribe únicamente la parte B con este texto:
```
