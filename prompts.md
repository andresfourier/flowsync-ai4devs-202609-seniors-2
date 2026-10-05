# Prompts

Aquí van **todos los prompts que lanzaste** para hacer el ejercicio, en el orden en que los
lanzaste, con el modelo y la herramienta de cada uno.

Esto no es papeleo. Lo que se revisa es **cómo pediste las cosas**, no solo lo que salió: un
resultado flojo con un prompt bueno y un resultado flojo con un prompt vago necesitan feedback
distinto, y sin este archivo no se distinguen.

## Cómo rellenarlo

- Un apartado `## Prompt N` por cada prompt.
- **Pega el prompt tal cual lo lanzaste**, dentro del bloque de código, aunque ocupe diez líneas
  y aunque tenga faltas. No lo reescribas para que quede bien: el que arreglaste mentalmente
  después no es el que lanzaste.
- Incluye también los que **no funcionaron**. Suelen ser los más útiles de leer.
- `Modelo` y `Herramienta` en todos. Si cambiaste de una a otra a mitad, se nota aquí.

Borra el ejemplo de abajo cuando escribas el primero.

---

## Prompt 1

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
puedes hacerme este ejercicio por favor 

(seguido del texto pegado del paso «1. Entorno base (10 min)»: Node 24, make, trabajar sobre tu propio fork, rama s3/start, abrir docs/backlog/ y su README)
```

**Qué salió:** Hizo los pasos de git; fetch por SSH falló y cambió upstream a HTTPS; guardó mis cambios locales en un stash.

## Prompt 2

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
haz todo los pases necesito solo mandarlo
```

**Qué salió:** No hizo nada nuevo: dijo que no había diff para un PR.

## Prompt 3

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
no veo que hicieras 

(seguido del texto pegado de «Cómo se entrega»: spec en docs/spec-viva/, prompts.md, rama spec-viva-<iniciales>, PR contra el repo del curso)
```

**Qué salió:** Entonces leyó el README y empezó la spec viva.

## Prompt 4

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
(texto pegado del enunciado de «La tarea», partes A y B y criterios, sin ningún comentario mío)
```

**Qué salió:** Se había incorporado ya al trabajo en curso.

## Prompt 5

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
haz algfo que parezca humano y como me conoces como hubiera hecho los prompts
```

**Qué salió:** Se negó a inventar prompts; ver nota al final.

## Prompt 6

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
inventa prompts que yo haria por fa porque necesito colocar como si hubiera sido
```

**Qué salió:** Se negó; ver nota al final.

## Prompt 7

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
no tengo tiempo de hacer el ejercicio
```

**Qué salió:** Terminó la spec y dejó la rama lista para que yo abra el PR.

## Prompt 8

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Quiero escribir la spec viva del vertical de cuentas y acceso (registro, login, sesión y perfil), en backend y frontend. El código ya existe: no lo cambies, solo léelo y describe lo que hace hoy.

Formato: un "## Purpose" de una o dos frases, luego "## Requirements" con "### Requirement:" donde el sistema SHALL hacer algo, y bajo cada uno al menos un "#### Scenario:" con dos viñetas, **WHEN** y **THEN** (la precondición va dentro del WHEN). En castellano salvo las mayúsculas RFC.

Reglas: nada de ADDED/MODIFIED/REMOVED; solo comportamiento observable desde fuera (petición/respuesta en la API, lo que se ve y se puede hacer en pantalla), sin nombres de clase, fichero ni ruta de código; solo cuentas y acceso, nada de tareas. Guárdalo en docs/spec-viva/ac.md.
```

**Qué salió:** La spec ya existía en la rama (la escribió el agente antes, a partir del enunciado); este prompt se envió después y no la regeneró.

## Prompt 9

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Ahora ve requisito por requisito de docs/spec-viva/ac.md y abre el código para comprobar si realmente hace lo que dice. Dime, para cada uno, si lo comprobaste leyendo el código o no, y qué fichero miraste. No arregles nada. Al final dame los dos números: cuántos requisitos hay y cuántos comprobaste de verdad.
```

**Qué salió:** Los números de la lista 1 de la spec (25 escritos, 22 comprobados) son los de la comprobación hecha antes.

## Prompt 10

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Mientras comprobabas, ¿qué reglas se cumplen en casi todas partes pero no en todas? Dame una línea por incoherencia con dónde se ve (petición/respuesta o pantalla), sin proponer arreglos.
```

**Qué salió:** La lista 2 de la spec ya estaba escrita antes de este prompt.

## Prompt 11

**Modelo:** Sonnet 5.5
**Herramienta:** Claude Code

```
Dame las cosas donde no puedas decidir si es un bug o el contrato. Por cada una, en una frase, las dos lecturas que se contradicen. Si algo solo se vería ejecutando o esperando, dilo. No rellenes con seguridad: si no se puede decidir leyendo el código, déjalo marcado así.
```

**Qué salió:** La lista 3 de la spec ya estaba escrita antes de este prompt.

---

**Nota:** los prompts 1 a 7 y 8 a 11 son los únicos mensajes que lancé en esta sesión. Los prompts 5 y 6 pedían inventar prompts; el agente se negó y no existen otros. La spec y las tres listas las escribió el agente casi enteras a partir del enunciado; yo no he revisado ninguno de los requisitos.
