# Demo 2: Agente en Accion

## Objetivo
Mostrar como un agente de codigo (Claude Code / OpenCode) planifica, ejecuta,
testea y corrige de forma autonoma — a diferencia de un chatbot que solo responde.

## Pre-requisitos
- Claude Code (`npm install -g @anthropic-ai/claude-code`) o
- OpenCode (`go install github.com/opencode-ai/opencode@latest`)
- Node.js 18+
- Un directorio vacio para el proyecto

## Ejercicio paso a paso

### Paso 1: Preparar el entorno
```bash
mkdir demo-agente && cd demo-agente
npm init -y
```

### Paso 2: Darle un objetivo al agente
Abrimos el agente y le damos esta instruccion:

```
Crea un endpoint REST en Express con TypeScript que:
1. POST /api/validate-email
2. Reciba { email: string } en el body
3. Valide con Zod
4. Responda { valid: boolean, error?: string }
5. Incluya tests con supertest y vitest
6. Agregue un script "test" en package.json
```

### Paso 3: Observar el loop del agente
Mientras el agente trabaja, observa estas fases:

1. **Planificacion**: El agente analiza que necesita hacer y en que orden
2. **Instalacion**: Ejecuta `npm install` con las dependencias necesarias
3. **Creacion**: Escribe los archivos de codigo
4. **Testing**: Corre los tests automaticamente
5. **Correccion**: Si algo falla, lee el error y corrige

Esto es el **loop Percibir → Pensar → Actuar → Observar**.

### Paso 4: Preguntate
- Un chatbot podria haber hecho esto?
- Que pasa si le decis "el test falla, arreglalo"?
- Cuantos archivos creo? Los leyo antes de modificarlos?

## Que observar
| Chatbot | Agente |
|---------|--------|
| Te da codigo para copiar | Escribe los archivos directamente |
| No sabe si funciona | Corre los tests |
| No corrige | Lee errores y se autocorrige |
| Sin contexto del proyecto | Lee archivos existentes |
| Una respuesta y listo | Loop iterativo hasta completar |

## Conclusion
La diferencia fundamental: el chatbot RESPONDE, el agente EJECUTA.
El agente tiene herramientas (filesystem, terminal, browser) y las usa
de forma autonoma para cumplir un objetivo.
