# barriodigital-contracts

Repositorio central de contratos de integración de la plataforma **BarrioDigital**.

## Descripción

Este repositorio contiene los contratos utilizados para definir la comunicación entre los distintos componentes de BarrioDigital.

El proyecto utiliza un enfoque:

```text
Contract First
```

Esto significa que los contratos son definidos y revisados antes de implementar la lógica de los servicios.

## Objetivos

- Definir APIs antes de su implementación.
- Permitir desarrollo paralelo entre frontend y backend.
- Evitar cambios de integración no controlados.
- Documentar modelos de request y response.
- Versionar contratos.
- Documentar eventos asíncronos.
- Mantener una fuente única de verdad de integración.

## Tecnologías

### APIs síncronas

```text
OpenAPI
```

Utilizado para documentar:

```text
REST / JSON
```

### Mensajería asíncrona

```text
AsyncAPI
```

Utilizado para documentar:

- RabbitMQ.
- Kafka.

### Schemas

```text
JSON Schema
```

cuando sea necesario reutilizar estructuras.

## Estructura

```text
barriodigital-contracts/
│
├── README.md
│
├── openapi/
│   ├── bff.openapi.yaml
│   ├── requests.openapi.yaml
│   ├── catalog.openapi.yaml
│   ├── crews.openapi.yaml
│   ├── audit.openapi.yaml
│   └── report.openapi.yaml
│
├── asyncapi/
│   ├── rabbitmq.asyncapi.yaml
│   └── kafka.asyncapi.yaml
│
├── schemas/
│   ├── common/
│   ├── requests/
│   ├── catalog/
│   ├── crews/
│   └── events/
│
└── docs/
    └── decisions/
```

## Versionamiento de APIs

Las APIs utilizarán versionamiento mediante path.

Versión inicial:

```text
/api/v1
```

Ejemplo:

```http
GET /api/v1/requests
```

Las modificaciones incompatibles deberán generar una nueva versión.

Ejemplo:

```text
/api/v2
```

## Servicios REST documentados

### BFF

```text
barriodigital-bff
```

Contrato:

```text
openapi/bff.openapi.yaml
```

### Requests

```text
ms-barriodigital-requests
```

Contrato:

```text
openapi/requests.openapi.yaml
```

### Catalog

```text
ms-barriodigital-catalog
```

Contrato:

```text
openapi/catalog.openapi.yaml
```

### Crews

```text
ms-barriodigital-crews
```

Contrato:

```text
openapi/crews.openapi.yaml
```

### Audit

```text
ms-barriodigital-audit
```

Contrato:

```text
openapi/audit.openapi.yaml
```

### Report

```text
ms-barriodigital-report
```

Contrato:

```text
openapi/report.openapi.yaml
```

## RabbitMQ

Contrato:

```text
asyncapi/rabbitmq.asyncapi.yaml
```

Flujos iniciales:

```text
q.cmd.email
q.cmd.crew
q.cmd.certificate
```

Dead Letter Queues:

```text
q.cmd.email.dlq
q.cmd.crew.dlq
q.cmd.certificate.dlq
```

Exchanges:

```text
cmd.direct
cmd.topic
cmd.dead.dlx
```

Routing keys iniciales:

```text
email.send
crew.ticket
certificate.gen
```

## Kafka

Contrato:

```text
asyncapi/kafka.asyncapi.yaml
```

Tópico principal:

```text
requests.events
```

Eventos iniciales:

```text
REQUEST_CREATED
REQUEST_ADMITTED
REQUEST_IN_PROGRESS
REQUEST_ON_SITE
REQUEST_RESOLVED
REQUEST_REJECTED
```

Otros tópicos considerados:

```text
audit.timeline
*.DLT
```

## Envelope común de eventos

Los eventos deberán utilizar una estructura común.

Ejemplo:

```json
{
  "eventId": "uuid",
  "type": "REQUEST_CREATED",
  "timestamp": "2026-09-05T13:30:00Z",
  "traceId": "trace-id",
  "correlationId": "REQ-2026-000001",
  "version": 1,
  "payload": {}
}
```

## Campos comunes

### eventId

Identificador único del evento.

### type

Tipo de evento o mensaje.

### timestamp

Fecha y hora de creación.

### traceId

Identificador utilizado para trazabilidad distribuida.

### correlationId

Identificador que permite relacionar mensajes pertenecientes a un mismo flujo de negocio.

### version

Versión del contrato del evento.

### payload

Contenido específico del evento.

## Principios

### Compatibilidad

Los cambios deben intentar mantener compatibilidad hacia atrás.

### Versionamiento

Los cambios incompatibles requieren nueva versión.

### Revisión

Los cambios de contrato deben realizarse mediante Pull Request.

### Fuente de verdad

Los contratos almacenados en este repositorio tienen prioridad sobre documentación informal.

## Flujo de trabajo

```text
Nueva funcionalidad
      ↓
Definir/modificar contrato
      ↓
Pull Request
      ↓
Revisión frontend + backend
      ↓
Merge
      ↓
Implementación
```

## Integración frontend/backend

El frontend debe implementar sus clientes basándose en OpenAPI.

Los servicios backend deben implementar los mismos contratos.

Esto permite desarrollar ambos lados en paralelo.

## Documentación de decisiones

Las decisiones arquitectónicas podrán mantenerse en:

```text
docs/decisions/
```

Formato recomendado:

```text
ADR-001-architecture.md
ADR-002-database-per-service.md
ADR-003-rabbitmq.md
ADR-004-kafka.md
ADR-005-cognito.md
```

Cada ADR deberá incluir:

```text
Contexto
Decisión
Alternativas
Consecuencias
```

## Estrategia Git

```text
main
develop
feature/*
fix/*
```

Los cambios de contrato deberán pasar por Pull Request.

## Estado

🚧 Contratos iniciales en proceso de definición.
