# odoo-windows-wsl
Entornos de desarrollo para Odoo en Windows con WSL

## WSL

El sistema que permite tener una capa de Linux en Windows 
se llama "Windows Subsystem for Linux" (WSL). 
WSL es una característica de Windows que permite ejecutar un entorno Linux 
completo, incluyendo un kernel de Linux, junto con Windows en la misma máquina
sin necesidad de una máquina virtual. 

Esto facilita la ejecución de aplicaciones y herramientas de Linux
directamente en un entorno Windows. WSL ofrece diferentes versiones, 
como WSL 1 y WSL 2, con diferentes niveles de compatibilidad y rendimiento.

### Comandos WSL en POWER SHELL

```` bash
# Muestra listado de distribuciones para instalar
wsl --list --online

# instala Ubuntu 
wsl --install -d Ubuntu-22.04

# ejemplo instalar debian 12
wsl --install -d Debian

# inicia una distribución
wsl -d Ubuntu-22.04

# tambien puedes iniciar por defecto
wsl

# eliminar una distri
wsl --unregister Ubuntu-22.04

````


## WSL v1 y v2

diferencias principales entre WSL 1 y WSL 2, cómo puedes pasar de WSL 1 a WSL 2 si lo deseas.

**Diferencias clave entre WSL 1 y WSL 2:**

1. **Arquitectura del núcleo:**
   - WSL 1: Utiliza una traducción dinámica para permitir que las aplicaciones de Linux se ejecuten en Windows sin un núcleo de Linux real. Esto significa que las aplicaciones se ejecutan en un espacio aislado, pero no tienen acceso directo al núcleo de Linux.
   - WSL 2: Utiliza una virtualización ligera basada en Hyper-V para ejecutar un núcleo de Linux completo dentro de una máquina virtual. Esto proporciona un mayor grado de compatibilidad con el núcleo de Linux y un mejor rendimiento en comparación con WSL 1.

2. **Compatibilidad del sistema de archivos:**
   - WSL 1: Utiliza un sistema de archivos traducido para acceder a los archivos de Windows desde el entorno de Linux. El rendimiento de las operaciones de E/S puede ser más lento.
   - WSL 2: Proporciona un sistema de archivos de Linux más completo y rápido que permite un acceso más rápido a los archivos y un mejor rendimiento en aplicaciones de Linux.

3. **Compatibilidad con contenedores:**
   - WSL 1: Puede ejecutar contenedores Docker, pero comparte el mismo espacio de nombres del núcleo que Windows.
   - WSL 2: Es compatible con contenedores Docker de manera más completa, ya que utiliza su propio espacio de nombres del núcleo.

4. **Rendimiento:**
   - WSL 2 generalmente ofrece un mejor rendimiento que WSL 1, especialmente en aplicaciones que realizan muchas operaciones de E/S o que requieren un alto rendimiento del núcleo de Linux.

**Cómo pasar de WSL 1 a WSL 2:**

Para cambiar de WSL 1 a WSL 2, sigue estos pasos:

1. Asegúrate de tener una versión de Windows 10 o Windows 11 que sea compatible con WSL 2. WSL 2 requiere Windows 10 versión 1903 o posterior, con actualizaciones de compilación específicas para la versión.

2. Abre PowerShell como administrador.

3. Ejecuta el siguiente comando para habilitar WSL 2:

   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```

4. Ejecuta el siguiente comando para habilitar la característica "Plataforma de máquina virtual":

   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

5. Reinicia tu computadora.

6. Descarga e instala la actualización del kernel de WSL 2 para Windows desde la siguiente ubicación:
   - [Actualización del kernel de WSL 2 para Windows](https://aka.ms/wsl2kernel)

7. Establece WSL 2 como la versión predeterminada para las distribuciones de Linux. Puedes hacerlo ejecutando el siguiente comando en PowerShell:

   ```powershell
   wsl --set-default-version 2
   ```

8. Ahora puedes actualizar tu distribución de Linux de WSL 1 a WSL 2. Abre tu distribución de Linux y ejecuta el siguiente comando:

   ```bash
   sudo dpkg --configure -a
   sudo apt-get update
   sudo apt-get dist-upgrade
   ```

Una vez completados estos pasos, habrás cambiado tu entorno de WSL de la versión 1 a la versión 2.

Ten en cuenta que, si tienes distribuciones de WSL 1 ya instaladas, deberás convertirlas a WSL 2 individualmente ejecutando el siguiente comando para cada distribución:

```bash
wsl --set-version <nombre_de_la_distribución> 2
wsl --set-version Ubuntu-22.04 2
```

Sustituye `<nombre_de_la_distribución>` por el nombre de la distribución que desees convertir.


Oficial Windows Upgrade Linux Kernel  
https://learn.microsoft.com/es-es/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

