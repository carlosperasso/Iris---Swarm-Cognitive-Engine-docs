# IRIS SCE — Swarm Cognitive Engine

🇪🇸 **Español** · [🇬🇧 English](README.en.md)

Un motor de razonamiento deliberativo: varios agentes deliberan sobre un material
declarado, el resultado se **audita de forma adversarial**, se mide cuánta credibilidad
tiene lo que salió, y **el informe se frena si se contradice con su propia auditoría**.

IRIS SCE no sabe de qué tema se está hablando. El tema entra desde afuera, en archivos de
configuración, y el motor no cambia.

---

## El problema

A un modelo de lenguaje se le pide un análisis y devuelve un texto plausible. Plausible
no es lo mismo que sostenido. IRIS SCE existe para poder mirar esa diferencia:

- separa lo **verificado** de lo **inferido** y de lo **no verificable**;
- pone a alguien a **refutar** el resultado, no a confirmarlo;
- convierte eso en **un solo número**, con sus motivos al lado;
- y si el texto final contradice lo que la auditoría encontró, no lo deja pasar como
  limpio.

## Tres decisiones que valen más que la arquitectura

1. **Sin auditoría no hay número.** Si nadie verificó ni cuestionó, la credibilidad es 0,
   con el motivo "no se auditó". Un puntaje inventado da confianza sin haberla ganado.
2. **Techo por respaldo.** Por buena que sea la deliberación, no puede superar el techo
   que le pone el material: si casi ningún hecho declara fuente, la conclusión no puede
   salir "sólida".
3. **Lo que falta, falta.** Ningún campo se completa por parecido ni se deduce del texto.
   Se pone el valor de reserva declarado y se avisa.

## Cómo funciona una corrida

```
Material declarado (pregunta + hechos con su fuente)
   │
   ├── producción   → agentes en paralelo, sin verse entre sí
   ├── auditoría    → uno etiqueta lo verificable, otro refuta; en paralelo
   │        └── medición de credibilidad con lo que hay hasta acá
   ├── cierre       → consolidación, solo si el puntaje habilita seguir
   │
   ├── candado de coherencia sobre el texto final
   └── Veredicto: credibilidad + coherencia + campos declarados + motivos
```

Cuatro **posturas** posibles, escritas una sola vez: producir, verificar, cuestionar,
consolidar. Describen cómo se para un agente frente a un material, nunca de qué habla.

Una **escalera** decide qué etapas correr antes de gastar un token, y permite entrar por
el medio reusando lo ya corrido. El **medidor** entrega un puntaje único con sus motivos.
El **candado de coherencia** revisa contradicciones sostenidas, objeciones altas sin
responder y material no verificado presentado como firme.

## Sin dominio, de verdad

- La función de entrada recibe el material y nada más: **ningún identificador externo**.
  El motor no abre bases de datos, no lee archivos de terceros y no consulta servicios.
  Si un dato no vino en el material, para el motor no existe.
- Los prompts describen **postura**, no asunto.
- Todo número que decide algo vive en configuración. El código no tiene constantes de
  criterio escritas adentro.
- Dar de alta un tema es escribir archivos de configuración y texto: **cero líneas de
  código**, nada se recompila y ningún módulo del motor se toca.
- **IRIS SCE es la marca, no un dominio**: el nombre no aparece dentro del motor.

## Estado

Versión 1.0.0. Python, sin dependencias más allá de un lector de configuración. Corre sin
red y sin credenciales contra un proveedor determinístico, para ejercitar orquestación,
medidor, candado y escalera; para hablar con un proveedor real, el endpoint entero se
describe desde afuera. Las credenciales nunca se escriben en la configuración: **se
nombran**, y el valor sale del entorno al momento de usarlo.

El código es privado. Este repositorio contiene únicamente este documento.
