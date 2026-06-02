# Portfolio de Ingeniería de Prompts: Automatización de Operaciones SaaS

## Proyecto 1: Sistema Avanzado de Clasificación y Respuesta de Soporte B2B
**Estado:** Producción / Prototipo Validado  
**Modelos Evaluados:** Gemini 1.5 Pro vs. Claude 3.5 Sonnet

### 1. El Problema de Negocio
"SyncTask", una empresa ficticia de software SaaS B2B ($49/mes por usuario), presentaba cuellos de botella en su departamento de soporte técnico y retención. Los correos de clientes críticos entraban en una bandeja genérica, retrasando la detección de usuarios en riesgo de cancelación (*churn*) y mezclando problemas técnicos urgentes con dudas de facturación menores.

### 2. La Solución (Arquitectura del Prompt)
Diseñé un "Megaprompt" estructurado por bloques lógicos ([ROL], [CONTEXTO], [TAREA]) para automatizar el triage de entrada. El objetivo es procesar el correo del cliente y obligar al modelo a devolver un objeto estructurado en formato **JSON** listo para ser consumido por un sistema automatizado de correos (CRM) o un equipo de desarrollo.

#### El Prompt Desarrollado:
```text
[ROL]
Actúa como un Ingeniero de Soporte Técnico Senior y Especialista en Retención de Clientes para la empresa de software "SyncTask" (SaaS de gestión de proyectos). Tu tono debe ser altamente profesional, empático, resolutivo y directo.

[CONTEXTO DE LA EMPRESA]
- SyncTask cuesta $49/mes por usuario.
- Política de Cancelación: Si un cliente quiere cancelar, se le debe ofrecer un mes gratis o una sesión de consultoría 1-on-1 antes de proceder.
- Política de Facturación: Si hay un cobro duplicado, se escala a finanzas y se promete una resolución en 24 horas.

[TAREA]
Analiza el correo electrónico del cliente adjunto abajo y genera un output estructurado en formato JSON con las siguientes claves:
1. "category": Clasifica el correo estrictamente en una de estas opciones: [Soporte Técnico, Facturación, Cancelación, Feedback].
2. "urgency_level": Asigna un nivel del 1 al 5 (donde 5 es crítico/pérdida de cliente).
3. "customer_sentiment": Describe brevemente el estado emocional del cliente (ej. Frustrado, Enojado, Confundido, Neutral).
4. "draft_response": Redacta una respuesta por correo electrónico en inglés que aplique técnicas de desescalada de conflictos. Si es facturación o cancelación, aplica las políticas de la empresa mencionadas en el contexto.

[CORREO DEL CLIENTE]
"Hi SyncTask team, I am extremely frustrated. Your platform has been down for the last two hours and my team couldn't access our project boards before a major client presentation. This is unacceptable for a service we pay $49/month for. I want a refund for this month, and honestly, if this happens again, I want to cancel my subscription immediately. Let me know how you will fix this."
