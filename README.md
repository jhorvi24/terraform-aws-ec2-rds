# Infraestructura en AWS con Terraform - Aplicación Web en Python Flask

![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/Amazon_AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)

---

### Descripción del Proyecto
Este repositorio contiene configuraciones de Terraform para implementar una infraestructura en AWS que aloja una aplicacion web con conexión a una base de datos relacional. La infraestructura incluye una instancia EC2 que ejecuta la aplicación web, una base de datos RDS, una red VPC y Systems Manager para la gestión de parametros de conexión a la base de datos. La aplicación web, desarrollada con el framework Flask de Python, se encuentra en otro repositorio en GitHub.

---

### Arquitectura
La infraestructura incluye:
- **VPC** con una subred pública y una subred privada.
- **Instancia EC2** ejecutando la aplicación Flask.
- **Base de datos RDS MariaDB** en una subred privada.
- **Systems Manager** para el almacenamiento seguro de los parámetros de conexion a la base de datos.
- **Grupos de seguridad** para el control de acceso a la red.

---

### Requisitos Previos
- Cuenta de AWS
- Terraform (versión >= 1.0.0)
- AWS CLI configurado
- Python 3.x
- Git

---

### Estructura del Repositorio
```
├──main.tf   
├──outputs.tf
├── .gitignore
└── README.md
```

---

### Componentes de la Infraestructura

#### Configuración de VPC
- VPC con un bloque CIDR especificado.
- Una subred pública y una subred privada en una zona de disponibilidad.
- Internet Gateway para acceso público.
- Tablas de enrutamiento para la gestión del tráfico de red.

#### Instancia EC2
- AMI de Amazon Linux 2023.
- Tipo de instancia t2.micro.
- Desplegada en una subred pública.
- Grupo de seguridad con acceso HTTP/SSH.
- User Data para la instalación de ciertos paquetes, la configuración de la aplicación web, la base de datos y su migración al servicio de RDS

#### Base de Datos RDS
- Motor MariaDB.
- Desplegada en un grupo de subredes privadas.
- Acceso seguro mediante grupos de seguridad.

#### Systems Manager
- Session Manager para acceso shell seguro.
- Parameter Store para la gestión de los parametros de conexión a la base de datos.


---

### Aplicación Web
- Aplicación usando el framwork Flask de Python .
- Conexión a la base de datos MariaDB.
- La aplicación web se encuentra en el repositorio: [Aplicación Web](https://github.com/jhorvi24/bookstore-python-flask.git)

---

### Instrucciones de Despliegue

1. **Clonar el Repositorio**
```bash
git clone <repository-url>
cd <repository-name>
```

2. **Inicializar Terraform**
```bash
cd terraform
terraform init
```

3. **Desplegar la Infraestructura**
```bash
terraform plan
terraform apply
```

---

### Consideraciones de Seguridad
- Instancias EC2 en subred pública con acceso restringido.
- RDS en subred privada.
- Grupos de seguridad con acceso mínimo necesario.
- Systems Manager para acceso seguro a las instancias y almacenamiento de parametros de conexión a la base de datos.

---

### Monitoreo y Mantenimiento
- Métricas y alarmas en CloudWatch.
- Systems Manager para aplicar parches.
- Copias de seguridad automáticas en RDS. (Se puede habilitar)


---


### Limpieza
Para destruir la infraestructura:
```bash
terraform destroy
```

---

### Contribuciones
1. Haz un fork del repositorio.
2. Crea una rama para tu funcionalidad.
3. Realiza tus cambios y haz un commit.
4. Sube los cambios a tu rama.
5. Crea un Pull Request.