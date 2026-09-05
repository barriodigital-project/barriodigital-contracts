# barriodigital-contracts

Repositorio central de contratos de integración de la plataforma **BarrioDigital**.

## Enfoque

```text
Contract First
```

Los contratos son definidos antes de implementar los microservicios.

## Tecnologías

### REST

```text
OpenAPI
```

### Mensajería

```text
AsyncAPI
```

## Estructura

```text
barriodigital-contracts/
│
├── README.md
│
├── openapi/
│   ├── requests.openapi.yaml
│   ├── catalog.openapi.yaml
│   ├── crews.openapi.yaml
│   ├── audit.openapi.yaml
│   ├── report.openapi.yaml
│   └── bff.openapi.yaml
│
└── asyncapi/
    ├── rabbitmq.asyncapi.yaml
    └── kafka.asyncapi.yaml
```

## OpenAPI

### Requests

```text
openapi/requests.openapi.yaml
```

Servicio:

```text
ms-barriodigital-requests
```

### Catalog

```text
openapi/catalog.openapi.yaml
```

Servicio:

```text
ms-barriodigital-catalog
```

### Crews

```text
openapi/crews.openapi.yaml
```

Servicio:

```text
ms-barriodigital-crews
```

### Audit

```text
openapi/audit.openapi.yaml
```

Servicio:

```text
ms-barriodigital-audit
```

### Report

```text
openapi/report.openapi.yaml
```

Servicio:

```text
ms-barriodigital-report
```

### BFF

```text
openapi/bff.openapi.yaml
```

Servicio:

```text
ms-barriodigital-bff
```

## RabbitMQ

Contrato:

```text
asyncapi/rabbitmq.asyncapi.yaml
```

Colas:

```text
q.cmd.notification
q.cmd.crew
```

Productor:

```text
ms-barriodigital-requests
```

Consumidor:

```text
ms-barriodigital-notify
```

## Kafka

Contrato:

```text
asyncapi/kafka.asyncapi.yaml
```

Tópico:

```text
requests.events
```

Productor:

```text
ms-barriodigital-requests
```

Consumidores:

```text
ms-barriodigital-audit
ms-barriodigital-report
```

Consumer Groups:

```text
barriodigital-audit-group
barriodigital-report-group
```

## Eventos

```text
REQUEST_CREATED
REQUEST_ADMITTED
REQUEST_RESOLVED
REQUEST_REJECTED
```

## Versionamiento

Las APIs utilizan:

```text
/api/v1
```

Versión inicial:

```text
1.0.0
```

## Flujo de trabajo

```text
Contrato
   ↓
Revisión
   ↓
Implementación
   ↓
Pruebas
```

Los cambios de integración deben reflejarse primero en este repositorio.

## Estrategia Git

```text
main
develop
feature/*
fix/*
```

## Estado

✅ Contratos V1 definidos.
