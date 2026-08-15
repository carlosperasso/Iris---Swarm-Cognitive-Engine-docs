<div align="center">

# IRIS SCE

### Swarm Cognitive Engine

*A domain-agnostic deliberative reasoning engine designed to produce conclusions that can be challenged, traced and audited.*

**[English](#english) · [Español](#espanol)**

</div>

---

<a name="english"></a>

## Overview

IRIS SCE coordinates multiple independent reasoning agents to analyze declared material from different positions.

Their conclusions are independently verified, challenged adversarially and measured against the available evidence.

A final coherence control prevents unsupported, contradictory or insufficiently audited conclusions from being presented as reliable.

> **IRIS does not guarantee that a conclusion is true.**
> It guarantees that the system exposes what supports it, what challenges it and what remains unknown.

---

## Why IRIS exists

A language model can produce a plausible answer without producing a supported answer.

IRIS separates:

- What was explicitly provided
- What was independently verified
- What was inferred
- What was challenged
- What could not be confirmed
- What remains unresolved

The objective is not to eliminate uncertainty.

**The objective is to prevent uncertainty from being hidden.**

---

## Execution model

```
                    Declared material
                            |
                            v
                    Execution policy
                            |
            +---------------+---------------+
            |                               |
            v                               v
  Independent production agents     Verification agent
            |                               |
            +---------------+---------------+
                            |
                            v
                  Adversarial challenge
                            |
                            v
              Evidence and objection analysis
                            |
                            v
                 Credibility measurement
                            |
              +-------------+-------------+
              |                           |
              v                           v
      Insufficient support          Consolidation
             Stop                         |
                                          v
                                   Coherence lock
                                          |
                            +-------------+-------------+
                            |                           |
                            v                           v
                  Contradiction detected         Audited result
                          Block
```

Production agents do not see each other's initial conclusions.

Verification and adversarial challenge are separate responsibilities.

A result is released only after its claims, evidence, objections and internal coherence have been evaluated.

---

## Core controls

### 1. No audit, no credibility

A result that has not been independently verified and challenged receives no credibility score.

Confidence must be earned through an explicit process.

### 2. Evidence sets the ceiling

The quality of the prose cannot raise a conclusion above the strength of its evidence.

If the declared material is weak, incomplete or poorly sourced, the final credibility must reflect that limitation.

### 3. Missing information stays missing

IRIS does not silently complete absent fields through resemblance, probability or narrative convenience.

Missing values remain explicitly marked as unresolved.

### 4. Adversarial challenge

One component is responsible for attempting to disprove the emerging conclusion.

Its responsibility is not to improve the wording or confirm consensus. Its responsibility is to identify:

- Unsupported claims
- Contradictions
- Weak evidence
- Alternative explanations
- Unresolved objections
- Excessive confidence

### 5. Coherence lock

The final report is checked against its own evidence and audit.

The coherence lock can block a result when:

- The conclusion contradicts verified evidence
- A major objection remains unanswered
- Inferred material is presented as verified
- Confidence exceeds the available support
- Different sections assert incompatible conclusions
- The audit does not justify the final result

---

## Domain isolation

IRIS does not contain business-specific knowledge inside its core.

The engine receives:

- Declared material
- Execution configuration
- Reasoning positions
- Thresholds and policies
- Provider configuration

It does not independently access client databases, private systems or undeclared sources.

**A new domain is introduced through configuration and declared material, not by modifying the reasoning engine.**

---

## Simplified public result contract

*The following example is an intentionally simplified public representation. It is not the private production schema.*

```json
{
  "conclusion": {
    "text": "The available evidence supports the claim with limitations.",
    "status": "supported_with_reservations",
    "credibility": 0.72
  },
  "claims": [
    {
      "claim_id": "claim-001",
      "statement": "Example factual assertion",
      "classification": "verified",
      "confidence": 0.86,
      "evidence": [
        {
          "source_id": "source-001",
          "retrieved_at": "2026-08-15T12:00:00Z",
          "supports_claim": true
        }
      ],
      "objections": []
    }
  ],
  "unresolved": [
    {
      "question": "Information required for stronger confirmation",
      "reason": "No declared source was available"
    }
  ],
  "audit": {
    "verification_completed": true,
    "adversarial_challenge_completed": true,
    "coherence_lock_passed": true
  }
}
```

The credibility value is not meaningful by itself.

It remains attached to:

- Evidence
- Objections
- Verification status
- Unresolved information
- Coherence controls

### Example of a blocked conclusion

```json
{
  "conclusion": {
    "status": "blocked",
    "credibility": 0
  },
  "block_reason": {
    "code": "COHERENCE_CONTRADICTION",
    "message": "The final conclusion contradicts verified evidence.",
    "affected_claims": [
      "claim-003",
      "claim-008"
    ]
  },
  "audit": {
    "verification_completed": true,
    "adversarial_challenge_completed": true,
    "coherence_lock_passed": false
  }
}
```

**IRIS does not rewrite the contradiction to make the report appear coherent.**

It blocks the result and exposes the reason.

---

## What IRIS guarantees

IRIS is designed to guarantee that:

- Declared material remains distinguishable from inferred material
- Missing information is not silently fabricated
- Verification and adversarial challenge are explicit stages
- Confidence is limited by evidence
- Major objections remain visible
- Contradictory final reports can be blocked
- The reasoning process leaves an auditable record

## What IRIS does not guarantee

IRIS does not guarantee:

- That every source is factually correct
- That every relevant source was provided
- That an external model will reason perfectly
- That a high-confidence conclusion is absolute truth
- That human review is unnecessary
- That domain-specific professional responsibility can be delegated to software

> IRIS controls the reasoning process.
> **It does not convert insufficient information into certainty.**

## What IRIS is not

IRIS is not:

- A search engine
- A general-purpose chatbot
- An automatic source of truth
- A replacement for qualified human responsibility
- A mechanism for converting unsupported statements into facts

*IRIS is an execution and control architecture for deliberative reasoning.*

---

## Architecture principles

The engine follows several structural principles:

| | |
|---|---|
| Independent production | Explicit verification |
| Adversarial refutation | Evidence-bounded confidence |
| Declared uncertainty | Internal coherence control |
| Provider separation | Domain isolation |
| Auditable execution | Deterministic testing where possible |

---

## Implementation status

IRIS SCE is implemented in Python.

Its orchestration, execution ladder, credibility controls and coherence mechanisms can be exercised without external network access through deterministic test providers.

External model providers are configured outside the reasoning core.

Credentials are referenced by name and obtained from the execution environment rather than stored inside configuration files.

---

## Repository scope

**The production source code is private.**

This repository provides public technical documentation describing:

- The purpose of the engine
- Its execution model
- Its architectural controls
- Its guarantees
- Its limitations
- A simplified public result contract

It does not contain:

- Production source code
- Private provider configuration
- Client information
- Credentials
- Internal operational data
- Proprietary scoring formulas

---

**Public documentation version:** 1.0.0

---

## Author

**Carlos Perasso**
Founder and Systems Architect at OrvixLabs
Argentina

## Links

- [OrvixLabs](https://orvixlabs.com)
- [IRIS SCE](https://iris-sce.com)
- [Carlos Perasso](https://carlosperasso.ar)

---

<div align="center">

# Versión en español

*Motor de razonamiento deliberativo, independiente del dominio, diseñado para producir conclusiones que puedan ser cuestionadas, rastreadas y auditadas.*

</div>

<a name="espanol"></a>

## Descripción general

IRIS SCE coordina múltiples agentes de razonamiento independientes para analizar material declarado desde distintas posiciones.

Sus conclusiones son verificadas de forma independiente, cuestionadas de manera adversarial y medidas contra la evidencia disponible.

Un control final de coherencia impide que conclusiones sin respaldo, contradictorias o insuficientemente auditadas se presenten como confiables.

> **IRIS no garantiza que una conclusión sea verdadera.**
> Garantiza que el sistema expone qué la sostiene, qué la cuestiona y qué permanece desconocido.

---

## Por qué existe IRIS

Un modelo de lenguaje puede producir una respuesta plausible sin producir una respuesta respaldada.

IRIS separa:

- Lo que fue provisto explícitamente
- Lo que fue verificado de forma independiente
- Lo que fue inferido
- Lo que fue cuestionado
- Lo que no pudo confirmarse
- Lo que permanece sin resolver

El objetivo no es eliminar la incertidumbre.

**El objetivo es impedir que la incertidumbre quede oculta.**

---

## Modelo de ejecución

```
                    Material declarado
                            |
                            v
                  Política de ejecución
                            |
            +---------------+---------------+
            |                               |
            v                               v
  Agentes de producción             Agente de
      independientes                verificación
            |                               |
            +---------------+---------------+
                            |
                            v
                Cuestionamiento adversarial
                            |
                            v
            Análisis de evidencia y objeciones
                            |
                            v
                Medición de credibilidad
                            |
              +-------------+-------------+
              |                           |
              v                           v
      Respaldo insuficiente         Consolidación
           Detener                         |
                                           v
                                  Candado de coherencia
                                           |
                            +--------------+--------------+
                            |                             |
                            v                             v
                  Contradicción detectada        Resultado auditado
                          Bloqueo
```

Los agentes de producción no ven las conclusiones iniciales de los demás.

La verificación y el cuestionamiento adversarial son responsabilidades separadas.

Un resultado se libera únicamente después de que sus afirmaciones, evidencia, objeciones y coherencia interna hayan sido evaluadas.

---

## Controles centrales

### 1. Sin auditoría, no hay credibilidad

Un resultado que no fue verificado y cuestionado de forma independiente no recibe puntaje de credibilidad.

La confianza debe ganarse a través de un proceso explícito.

### 2. La evidencia define el techo

La calidad de la redacción no puede elevar una conclusión por encima de la solidez de su evidencia.

Si el material declarado es débil, incompleto o mal referenciado, la credibilidad final debe reflejar esa limitación.

### 3. Lo que falta, sigue faltando

IRIS no completa silenciosamente campos ausentes por semejanza, probabilidad o conveniencia narrativa.

Los valores faltantes permanecen marcados explícitamente como no resueltos.

### 4. Cuestionamiento adversarial

Un componente tiene la responsabilidad de intentar refutar la conclusión emergente.

Su responsabilidad no es mejorar la redacción ni confirmar el consenso. Su responsabilidad es identificar:

- Afirmaciones sin respaldo
- Contradicciones
- Evidencia débil
- Explicaciones alternativas
- Objeciones sin resolver
- Confianza excesiva

### 5. Candado de coherencia

El informe final se contrasta contra su propia evidencia y su auditoría.

El candado de coherencia puede bloquear un resultado cuando:

- La conclusión contradice evidencia verificada
- Una objeción mayor permanece sin responder
- Material inferido se presenta como verificado
- La confianza excede el respaldo disponible
- Distintas secciones afirman conclusiones incompatibles
- La auditoría no justifica el resultado final

---

## Aislamiento del dominio

IRIS no contiene conocimiento específico de negocio dentro de su núcleo.

El motor recibe:

- Material declarado
- Configuración de ejecución
- Posturas de razonamiento
- Umbrales y políticas
- Configuración de proveedores

No accede por su cuenta a bases de datos de clientes, sistemas privados ni fuentes no declaradas.

**Un dominio nuevo se introduce mediante configuración y material declarado, no modificando el motor de razonamiento.**

---

## Contrato público simplificado del resultado

*El siguiente ejemplo es una representación pública intencionalmente simplificada. No es el esquema privado de producción.*

```json
{
  "conclusion": {
    "text": "La evidencia disponible respalda la afirmación con limitaciones.",
    "status": "supported_with_reservations",
    "credibility": 0.72
  },
  "claims": [
    {
      "claim_id": "claim-001",
      "statement": "Afirmación fáctica de ejemplo",
      "classification": "verified",
      "confidence": 0.86,
      "evidence": [
        {
          "source_id": "source-001",
          "retrieved_at": "2026-08-15T12:00:00Z",
          "supports_claim": true
        }
      ],
      "objections": []
    }
  ],
  "unresolved": [
    {
      "question": "Información requerida para una confirmación más sólida",
      "reason": "No hubo fuente declarada disponible"
    }
  ],
  "audit": {
    "verification_completed": true,
    "adversarial_challenge_completed": true,
    "coherence_lock_passed": true
  }
}
```

El valor de credibilidad no es significativo por sí solo.

Permanece atado a:

- Evidencia
- Objeciones
- Estado de verificación
- Información sin resolver
- Controles de coherencia

### Ejemplo de una conclusión bloqueada

```json
{
  "conclusion": {
    "status": "blocked",
    "credibility": 0
  },
  "block_reason": {
    "code": "COHERENCE_CONTRADICTION",
    "message": "La conclusión final contradice evidencia verificada.",
    "affected_claims": [
      "claim-003",
      "claim-008"
    ]
  },
  "audit": {
    "verification_completed": true,
    "adversarial_challenge_completed": true,
    "coherence_lock_passed": false
  }
}
```

**IRIS no reescribe la contradicción para que el informe parezca coherente.**

Bloquea el resultado y expone el motivo.

---

## Qué garantiza IRIS

IRIS está diseñado para garantizar que:

- El material declarado permanece distinguible del material inferido
- La información faltante no se fabrica silenciosamente
- La verificación y el cuestionamiento adversarial son etapas explícitas
- La confianza está limitada por la evidencia
- Las objeciones mayores permanecen visibles
- Los informes finales contradictorios pueden bloquearse
- El proceso de razonamiento deja un registro auditable

## Qué no garantiza IRIS

IRIS no garantiza:

- Que toda fuente sea fácticamente correcta
- Que se haya provisto toda fuente relevante
- Que un modelo externo razone perfectamente
- Que una conclusión de alta confianza sea verdad absoluta
- Que la revisión humana sea innecesaria
- Que la responsabilidad profesional específica del dominio pueda delegarse en software

> IRIS controla el proceso de razonamiento.
> **No convierte información insuficiente en certeza.**

## Qué no es IRIS

IRIS no es:

- Un motor de búsqueda
- Un asistente conversacional de propósito general
- Una fuente automática de verdad
- Un reemplazo de la responsabilidad humana calificada
- Un mecanismo para convertir afirmaciones sin respaldo en hechos

*IRIS es una arquitectura de ejecución y control para razonamiento deliberativo.*

---

## Principios de arquitectura

El motor sigue varios principios estructurales:

| | |
|---|---|
| Producción independiente | Verificación explícita |
| Refutación adversarial | Confianza limitada por evidencia |
| Incertidumbre declarada | Control interno de coherencia |
| Separación de proveedores | Aislamiento del dominio |
| Ejecución auditable | Pruebas deterministas donde es posible |

---

## Estado de implementación

IRIS SCE está implementado en Python.

Su orquestación, escalera de ejecución, controles de credibilidad y mecanismos de coherencia pueden ejercitarse sin acceso a red externa mediante proveedores de prueba deterministas.

Los proveedores de modelos externos se configuran fuera del núcleo de razonamiento.

Las credenciales se referencian por nombre y se obtienen del entorno de ejecución, en lugar de almacenarse dentro de archivos de configuración.

---

## Alcance del repositorio

**El código fuente de producción es privado.**

Este repositorio provee documentación técnica pública que describe:

- El propósito del motor
- Su modelo de ejecución
- Sus controles arquitectónicos
- Sus garantías
- Sus limitaciones
- Un contrato público simplificado del resultado

No contiene:

- Código fuente de producción
- Configuración privada de proveedores
- Información de clientes
- Credenciales
- Datos operativos internos
- Fórmulas propietarias de puntuación

---

**Versión de la documentación pública:** 1.0.0

---

## Autor

**Carlos Perasso**
Founder and Systems Architect en OrvixLabs
Argentina

## Enlaces

- [OrvixLabs](https://orvixlabs.com)
- [IRIS SCE](https://iris-sce.com)
- [Carlos Perasso](https://carlosperasso.ar)
