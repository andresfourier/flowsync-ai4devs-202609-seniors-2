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

---

**Nota:** estos son los únicos mensajes que lancé en esta sesión. Los prompts 5 y 6 pedían inventar prompts; el agente se negó y no existen otros. La spec y las tres listas las escribió el agente casi enteras a partir del enunciado; yo no he revisado ninguno de los requisitos.
