# Laboratorio 02 — Infraestructura como código

Comparación de Terraform (HCL) y Pulumi (Python) para desplegar Nginx en Docker local. Cada implementación administra su propia red, imagen y contenedor.

## Nombres y roles

**Grupo 07**

| Integrante | Rol | Responsabilidad |
|---|---|---|
| David Alexander Zambrano B. | R1 — Terraform | Implementación y validación del despliegue con Terraform. |
| Jose David Anacona Pira | R2 — Pulumi | Implementación y validación del despliegue con Pulumi. |
| David Alexander Zambrano B. y Jose David Anacona Pira | R3 — Platform Lead | Integración, CI y análisis comparativo de ambas herramientas. |

## Requisitos

- Git.
- Docker Engine o Docker Desktop iniciado y configurado para contenedores Linux.
- Terraform >= 1.5.0 para la implementación HCL.
- Python 3.11 y Pulumi CLI 3.x para la implementación Python.
- Puertos locales `8080` y `8090` disponibles.
- Acceso a Internet para descargar proveedores, dependencias e imágenes.

Los comandos siguientes se ejecutan en **PowerShell**, desde la raíz de una copia del repositorio que contenga las carpetas `terraform/` y `pulumi/`. Verifica primero la conexión con Docker:

```powershell
docker info
```

## Despliegue local con Terraform

Entra en la carpeta y copia la configuración de ejemplo, solo si todavía no tienes un archivo `terraform.tfvars`:

```powershell
cd terraform
Copy-Item terraform.tfvars.example terraform.tfvars
```

Edita `terraform.tfvars` con estos valores para el grupo 07:

```hcl
group_id      = "grupo07"
environment   = "dev"
host_port     = 8080
nginx_version = "1.27-alpine"
```

Inicializa el proveedor, valida la configuración y revisa el plan antes de aplicar:

```powershell
terraform init
terraform validate
terraform plan
terraform apply
terraform output
```

Confirma el despliegue escribiendo `yes` cuando se solicite. El contenedor se llamará `servidor-web-grupo07-tf` y el servicio estará disponible en [http://127.0.0.1:8080](http://127.0.0.1:8080).

```powershell
(Invoke-WebRequest -Uri http://127.0.0.1:8080).StatusCode
```

El resultado esperado es `200`. Para eliminar los recursos administrados por esta implementación, ejecuta desde `terraform/` y confirma la operación:

```powershell
terraform destroy
```

## Despliegue local con Pulumi

Desde la raíz del repositorio, crea el entorno virtual e instala las dependencias:

```powershell
cd pulumi
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
pulumi login --local
pulumi stack init local
```

Define y conserva la contraseña de cifrado cuando Pulumi la solicite. Se utiliza un stack nuevo llamado `local`, separado del archivo `Pulumi.dev.yaml` incluido en el repositorio. Si ya creaste este stack en tu equipo, usa `pulumi stack select local` en lugar de inicializarlo otra vez. El backend local guarda el estado en tu equipo; consulta la [documentación de backends de Pulumi](https://www.pulumi.com/docs/iac/concepts/state-and-backends/).

Configura el stack y revisa los cambios antes de desplegar:

```powershell
pulumi config set groupId grupo07
pulumi config set environment dev
pulumi config set hostPort 8090
pulumi config set nginxVersion 1.27-alpine
pulumi preview --refresh
pulumi up --refresh
pulumi stack output
```

Confirma el despliegue seleccionando `yes`. El contenedor se llamará `servidor-web-grupo07-pulumi` y el servicio estará disponible en [http://127.0.0.1:8090](http://127.0.0.1:8090).

```powershell
(Invoke-WebRequest -Uri http://127.0.0.1:8090).StatusCode
```

El resultado esperado es `200`. Para eliminar los recursos del stack seleccionado, ejecuta desde `pulumi/` y confirma la operación:

```powershell
pulumi destroy
```

Ambas implementaciones conservan la imagen Nginx descargada en Docker después de destruir los recursos (`keep_locally = true`).

## Informe y evidencias

La matriz comparativa, las evidencias de detección de drift y la conclusión arquitectónica están en [el informe comparativo](docs/informe_comparativo.md).
