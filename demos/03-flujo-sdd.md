# Demo 3: Flujo Spec-Driven Development (SDD)

## Objetivo
Mostrar como se trabaja profesionalmente con agentes: no se improvisa,
se escribe una spec PRIMERO y despues el agente ejecuta.

## Concepto clave
**SDD = Spec-Driven Development**
En vez de decirle al agente "haceme X" de forma improvisada, le das un
documento estructurado que define QUE hacer, COMO hacerlo y cuales son
los criterios de aceptacion. El agente se convierte en un ejecutor de specs.

## Ejercicio paso a paso

### Paso 1: Escribir la spec
Crea un archivo `spec.md` con esta estructura:

```markdown
# Spec: API de Notas

## Objetivo
Crear una API REST para gestionar notas personales.

## Contexto
- Stack: Express + TypeScript + SQLite (mejor-sqlite3)
- Sin autenticacion (MVP)
- Puerto 3000

## Requisitos funcionales
1. GET /api/notes — listar todas las notas
2. POST /api/notes — crear nota { title: string, body: string }
3. GET /api/notes/:id — obtener nota por ID
4. DELETE /api/notes/:id — eliminar nota

## Restricciones
- Validacion con Zod en todos los endpoints
- Respuestas estandarizadas: { data: T } o { error: string }
- Tests con vitest + supertest (minimo 1 test por endpoint)
- Base de datos SQLite en archivo `data/notes.db`

## Criterios de aceptacion
- [ ] Todos los endpoints responden correctamente
- [ ] Los tests pasan con `npm test`
- [ ] El proyecto se inicia con `npm start`
- [ ] Zod rechaza payloads invalidos con error 400
```

### Paso 2: Pasarsela al agente
```
Lee el archivo spec.md y ejecuta todo lo que dice.
Segui el orden: setup → base de datos → endpoints → tests.
Cuando termines, correme los tests.
```

### Paso 3: Observar la ejecucion
El agente deberia:
1. Leer la spec completa
2. Planificar el orden de ejecucion
3. Crear el proyecto y las dependencias
4. Implementar la base de datos
5. Crear los endpoints uno por uno
6. Escribir y correr los tests
7. Reportar si los criterios de aceptacion se cumplen

### Paso 4: Iterar
Si algo no cumple la spec, decile:
```
El endpoint DELETE no devuelve 404 cuando la nota no existe.
Arreglalo segun la spec.
```

El agente lee la spec, entiende el gap, y corrige.

## Flujo visual

```
Spec (humano)  →  Agente lee spec  →  Planifica  →  Ejecuta
                                                        ↓
                    Humano revisa  ←  Tests pasan  ←  Testea
                        ↓
                  ¿Cumple spec?
                   Si → Merge
                   No → Iterar
```

## Conclusion
El codigo ya no se escribe de cero: se DIRIGE.
La spec es el nuevo "codigo fuente" del proceso.
El humano define QUE, el agente resuelve COMO.
Esto es Spec-Driven Development.
