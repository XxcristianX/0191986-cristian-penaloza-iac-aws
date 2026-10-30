# Taller Práctico: Despliegue de EC2 con GitHub Actions y CloudFormation

**Asignatura:** Cloud Computing  
**Programa Académico:** Ingeniería de Sistemas  
**Institución:** Universidad Francisco de Paula Santander Ocaña (UFPSO)  
**Docente Titular:** Wilder Andrés Duarte Neira  
**Estudiante:** Cristian Eduardo Peñaloza Granados  
**Código Estudiantil:** 0191986  

---

## 1. Descripción del Proyecto
Este proyecto implementa una solución de **Infraestructura como Código (IaC)** en Amazon Web Services (AWS). A través de una plantilla declarativa en **AWS CloudFormation** y un pipeline de Integración y Despliegue Continuo (CI/CD) orquestado por **GitHub Actions**, se aprovisiona automáticamente una máquina virtual **Amazon EC2** con servidor web **Apache HTTPD** configurado para servir una página web personalizada.

---

## 2. Estructura del Repositorio
```
0191986-cristian-penaloza-iac-aws/
├── .github/
│   └── workflows/
│       └── deploy.yml          # Flujo automatizado de despliegue en GitHub Actions
├── templates/
│   └── template.yaml        # Plantilla CloudFormation (EC2, Security Group, User Data)
└── README.md                # Documentación institucional y especificaciones técnicas
```

---

## 3. Arquitectura y Componentes en AWS
- **Stack de CloudFormation:** `proyecto-web-iac`.
- **Instancia EC2:** `t2.micro` (Capa gratuita) con sistema operativo Amazon Linux 2023.
- **Grupo de Seguridad:** `SG-HTTP-0191986-CF` con tráfico entrante TCP habilitado únicamente en el puerto 80 (HTTP) para todo Internet (`0.0.0.0/0`).
- **User Data Script:** Instalación desatendida de Apache (`yum install -y httpd`), activación como servicio de arranque (`systemctl enable httpd`) y creación dinámica del archivo `/var/www/html/index.html`.
- **Pipeline CI/CD:** Ejecución automática en cada `push` hacia la rama `main` autenticado de manera segura con secretos de repositorio (`AWS_ACCESS_KEY_ID` y `AWS_SECRET_ACCESS_KEY`).

---

## 4. Enlace del Sitio Web Desplegado
Una vez completado el flujo en GitHub Actions y creado el Stack en AWS, el servidor web puede ser visitado en:
- **URL Pública:** `http://[IP_PUBLICA_EC2]`
*(Reemplazar con la dirección IP pública consultada en la consola de AWS EC2 o en las salidas del Stack).*

---

## 5. Control de Modificaciones y Actualizaciones (Punto 8)
- **Versión 1.0:** Despliegue inicial del servidor Apache con la estructura base de presentación.
- **Versión 2.0:** Actualización de estilos visuales, etiquetas de gestión de infraestructura y contenido HTML mediante nuevo commit en GitHub Actions.
