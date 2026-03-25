# Demo 1: Prompting Profesional

## Objetivo
Comparar un prompt vago contra un prompt profesional estructurado y ver la diferencia en la calidad de la respuesta.

## Ejercicio paso a paso

### Paso 1: El prompt vago
Abri tu LLM favorito (ChatGPT, Claude, Ollama) y escribi:

```
haceme una funcion que valide emails
```

Observa la respuesta. Probablemente funcione, pero:
- No sabes en que lenguaje lo queres
- No sabes que reglas de validacion aplica
- No sabes si maneja edge cases
- No tiene tests

### Paso 2: El prompt profesional (5 capas)
Ahora usa la estructura de 5 capas:

```markdown
## System
Sos un senior TypeScript developer. Seguis principios SOLID y escribis
codigo production-ready con tests.

## Contexto
Estoy construyendo un formulario de registro para una app Next.js.
Necesito validar emails antes de enviarlos al backend.
Usamos Zod para validacion.

## Instruccion
Crea una funcion `validateEmail` que:
1. Valide formato RFC 5322 basico
2. Rechace dominios temporales (mailinator, guerrillamail, etc)
3. Retorne un objeto tipado con `{ valid: boolean, error?: string }`

## Formato
- TypeScript con tipos explicitos
- Schema Zod para la validacion
- Tests con Vitest (minimo 5 casos)
- Exporta desde un archivo `email-validator.ts`

## Ejemplos
Input: "usuario@gmail.com" → { valid: true }
Input: "noarroba" → { valid: false, error: "Formato invalido" }
Input: "test@mailinator.com" → { valid: false, error: "Dominio temporario" }
```

### Paso 3: Compara
Pone las dos respuestas lado a lado. Preguntate:
- Cual esta lista para produccion?
- Cual tiene tests?
- Cual maneja edge cases?
- Cual documentarias con confianza?

## Conclusion
El prompt ES codigo. Prompt vago = `any`. Prompt profesional = tipos estrictos.
La calidad del output es directamente proporcional a la calidad del input.
