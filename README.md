# Guía de Estructura de Micro-Laboratorios — PternaSec/vuln-labs

Este repositorio almacena los contenedores Docker locales (Micro-Labs) que se utilizan e inician exclusivamente a través de la **PternaSec CLI**. No está pensado para uso manual, sino como fuente de datos para nuestra herramienta de línea de comandos.

## Estructura de Directorios

```
vuln-labs/
├── log4shell/              ← Nombre/Slug del laboratorio (slug único)
│   ├── README.md           ← OBLIGATORIO (con Frontmatter YAML)
│   └── docker-compose.yml  ← Altamente recomendado para despliegue automatizado
└── shellshock/
    ├── README.md
    └── docker-compose.yml
```

---

## Formato del README.md (Frontmatter YAML)

Cada subcarpeta de laboratorio debe contener un `README.md` con un bloque superior Frontmatter YAML delimitado por `---` para definir las propiedades:

```markdown
---
title: "Log4Shell Lab"
description: "Entorno interactivo para la explotación segura de la inyección JNDI en Log4j."
type: docker # Puede ser "docker" (CLI) o "cloud" (TryHackMe/Web)
difficulty: advanced # beginner, intermediate, advanced, expert
author: "PternaSec"
category: rce
script: log4shell
requirements:
  - Docker
  - Docker Compose
docker_image: "pternasec/log4shell:vuln"
---

## Instrucciones de Despliegue (Vía CLI)

**No es necesario clonar este repositorio ni ejecutar Docker manualmente.**

Para iniciar cualquier laboratorio, utiliza nuestra herramienta de consola:
1. Instala la CLI: `npm install -g pternasec-cli` (Próximamente)
2. Ejecuta el comando en tu terminal: `pterna lab start <slug-del-lab>`
3. La herramienta se encargará de descargar el `docker-compose.yml`, configurarlo y levantarlo automáticamente.

Ejemplo:
```bash
pterna lab start log4shell
```

---

## Opciones Disponibles para los Campos

### 1. Categorías (`category`)
Asocia el laboratorio a una temática de ciberseguridad. Opciones de categorías soportadas (en minúsculas):
- `rce` (Remote Code Execution)
- `sqli` (SQL Injection)
- `xss` (Cross-Site Scripting)
- `lfi` (File Inclusion)
- `ssrf` (Server-Side Request Forgery)
- `csrf` (Cross-Site Request Forgery)
- `xxe` (XML External Entity)
- `path-traversal` (Path Traversal)
- `cmd-injection` (Command Injection)
- `buffer-overflow` (Buffer Overflow)
- `priv-esc` (Privilege Escalation)
- `auth` (Authentication Bypass)
- `crypto` (Crypto)
- `deserialization` (Insecure Deserialization)
- `idor` (Insecure Direct Object Reference)
- `open-redirect` (Open Redirect)
- `race-condition` (Race Condition)
- `cors` (Cross-Origin Resource Sharing)
- `prototype-pollution` (Prototype Pollution)
- `ssti` (Server-Side Template Injection)
- `crlf` (CRLF Injection)
- `http-smuggling` (HTTP Request Smuggling)
- `graphql` (GraphQL Vulnerability)
- `websockets` (WebSockets Vulnerability)
- `uaf` (Use After Free / Binary Vulnerabilities)

### 2. Relación con Script (`script`)
Debe coincidir exactamente con el **slug del exploit** relacionado en el repositorio `scripts` (ej. `log4shell`). Esto permite enlazar la guía interactiva del exploit con el arranque de este contenedor.

### 3. Requerimientos (`requirements`)
Es una lista YAML de software necesario para levantar el entorno. Comúnmente:
- `Docker`
- `Docker Compose`
- `Python 3.x`
- `Java JDK`

### 4. Imagen de Docker (`docker_image` - Opcional)
Define la imagen pre-construida oficial de Docker (ej. `pternasec/log4shell:vuln`). Útil para que los usuarios puedan descargarla sin necesidad de compilar localmente.
