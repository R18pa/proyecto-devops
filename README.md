#  Proyecto Final — Infraestructura DevOps en la Nube

**Sistemas Operativos II — Universidad Mariano Galvez de Guatemala**

| Campo | Detalle |
|-------|---------|
| **Estudiante** | David Alejandro Rodriguez Flores |
| **Carné** | 0910-23-1765 |
| **Catedrático** | Lic. Erick Orlando Ovando Castillo |
| **Fecha** | 30 de mayo de 2026 |

---

## 📋 Descripción

Implementación de una infraestructura moderna basada en prácticas **DevOps** utilizando servicios en la nube de **Amazon Web Services (AWS)**. El proyecto despliega una aplicación web contenerizada con **Docker**, orquestada con **Docker Swarm**, y con un pipeline **CI/CD** completamente automatizado mediante **GitHub Actions**.

La aplicación está disponible en: **http://18.223.160.3:8080**

---

## 🛠️ Tecnologías Utilizadas

| Categoría | Tecnología |
|-----------|-----------|
| Contenedores | Docker 25.0.14 |
| Orquestación | Docker Swarm |
| CI/CD | GitHub Actions |
| Control de versiones | GitHub |
| Infraestructura Cloud | AWS EC2 t3.micro |
| Servidor Web | Nginx Alpine |
| Monitoreo | Amazon CloudWatch |
| Sistema Operativo | Amazon Linux 2023 |

---

## 📁 Estructura del Repositorio

```
proyecto-devops/
├── .github/
│   └── workflows/
│       └── deploy.yml      # Pipeline CI/CD automatizado
├── app/
│   └── index.html          # Aplicación web BMW
├── Dockerfile              # Definición de la imagen Docker
├── docker-compose.yml      # Configuración de servicios
└── README.md               # Este archivo
```

---

## ⚙️ Configuración de la Infraestructura

### AWS EC2
- **Instancia:** i-004011599a94aa24d
- **Tipo:** t3.micro (Free Tier)
- **Región:** us-east-2 (Ohio)
- **IP Pública:** 18.223.160.3
- **SO:** Amazon Linux 2023

### Seguridad
- Acceso SSH mediante par de llaves RSA (.pem)
- Security Group con puertos 22 (SSH) y 8080 (HTTP)
- Secretos de GitHub Actions para credenciales cifradas

---

## 🐳 Docker

### Construir la imagen localmente
```bash
docker build -t bmw-web .
```

### Correr con Docker Compose
```bash
docker compose up --build -d
```

### Verificar contenedor
```bash
docker ps
```

Acceder en: http://localhost:8080

---

## 🔄 Pipeline CI/CD

El pipeline se activa automáticamente con cada `push` a la rama `master` y ejecuta las siguientes etapas:

```
Push a master
     │
     ▼
1. Clonar repositorio
     │
     ▼
2. Construir imagen Docker
     │
     ▼
3. Pruebas básicas (curl localhost:8080)
     │
     ▼
4. Despliegue automático en AWS via SSH
     │
     ▼
App actualizada en producción ✅
```

### Secretos requeridos en GitHub Actions

| Secreto | Descripción |
|---------|-------------|
| `EC2_HOST` | IP pública del servidor AWS |
| `EC2_USER` | Usuario de la instancia (ec2-user) |
| `EC2_KEY` | Llave privada RSA para SSH |

---

## 🌐 Docker Swarm

```bash
# Inicializar el Swarm
docker swarm init

# Desplegar el servicio
docker service create --name bmw-web --publish 8080:80 bmw-web

# Ver estado del servicio
docker service ls

# Ver nodos del cluster
docker node ls
```

---

## 📊 Monitoreo

El monitoreo se realiza mediante **Amazon CloudWatch** con monitoreo detallado habilitado en la instancia EC2. Métricas disponibles:

- Utilización de CPU (%)
- Entrada/Salida de red (bytes)
- Paquetes de red
- Operaciones de disco

---

## 🔧 Instalación Local

### Requisitos previos
- Git
- Docker Desktop
- AWS CLI
- kubectl

### Pasos
```bash
# 1. Clonar el repositorio
git clone https://github.com/R18pa/proyecto-devops.git
cd proyecto-devops

# 2. Construir y correr
docker compose up --build -d

# 3. Abrir en el navegador
# http://localhost:8080
```

---

## 📄 Documentación

El documento técnico completo en formato PDF está disponible en la carpeta del proyecto e incluye:

- Diseño arquitectónico con diagramas
- Configuración detallada de AWS
- Explicación del pipeline CI/CD
- Evidencias y capturas de pantalla
- Conclusiones y aprendizajes
- Referencias en formato APA

---

## 👤 Autor

**David Alejandro Rodriguez Flores**  
Carné: 0910-23-1765  
Universidad Mariano Galvez de Guatemala  
Sistemas Operativos II — 2026
