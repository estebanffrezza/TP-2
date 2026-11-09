# Reporte Técnico: Mi Primer Laboratorio Seguro
## Guía de Instalación Paso a Paso y Configuración Avanzada de Red

Este repositorio contiene la documentación técnica y las evidencias obligatorias correspondientes a la **Pre-entrega 2** del curso de Ciberseguridad de Coderhouse.

---

## 1. Concepto Fundamental: ¿Qué es un Entorno Aislado?
Un entorno aislado es un ambiente de pruebas separado del sistema operativo principal [cite: 2]. Permite realizar prácticas de ciberseguridad, instalar software peligroso y efectuar configuraciones de riesgo sin afectar de ninguna manera al equipo anfitrión (Host) [cite: 2]. Actúa como una caja de arena (*sandbox*) digital donde el malware o las malas configuraciones quedan completamente contenidos en una capa virtual [cite: 1].

---

## 2. Guía de Instalación Paso a Paso (Secuencia del Proceso)

### Paso 1: Instalación del Hipervisor e Inicialización
1. Descarga del binario ejecutable oficial de `Oracle VirtualBox 7.2.22` para arquitectura `amd64` [cite: 2].
2. Aceptación de los términos de la Licencia de Usuario Final (GPL v3) [cite: 2].
3. Configuración personalizada de características (*Custom Setup*) incluyendo soporte USB, componentes de red esenciales y bindings de Python [cite: 2].
4. Aceptación del aviso de desconexión temporal de red física necesaria para compilar las interfaces virtuales del hipervisor [cite: 2].

<!-- REEMPLAZA ESTA RUTA POR TU CAPTURA DE INSTALACIÓN REAL -->
![Evidencia 1 - Instalación de VirtualBox](img/instalacion.png)

### Paso 2: Creación y Aprovisionamiento del Hardware Virtual
1. Inicialización del Administrator de VirtualBox y selección de la opción **"Nueva"** [cite: 2].
2. Asignación del nombre unívoco de la máquina virtual: `PCII` [cite: 2].
3. Montaje del archivo de imagen de disco óptico (ISO) oficial de `Windows 11 Client x64` [cite: 2].
4. Habilitación de la casilla *"Proceed with Unattended Installation"* para automatizar los parámetros básicos [cite: 2].
5. **Asignación de Recursos Críticos:** Provisión de hardware asignando **15808 MB de Memoria Base (aprox. 15 GB RAM)** y **11 núcleos de procesamiento CPU**, activando el entorno de firmware **EFI** para cumplir con las exigencias nativas del sistema operativo moderno [cite: 2].

<!-- REEMPLAZA ESTA RUTA POR TU CAPTURA DE HARDWARE REAL -->
![Evidencia 2 - Hardware Asignado PCII](img/hardware.png)

### Nota de Arquitectura (Justificación de Recursos)
Se determinó una asignación masiva de **15,808 MB de RAM** y **11 núcleos de vCPU** debido a que este entorno no se limitará a ser una máquina cliente de uso simple [cite: 2]. Esta infraestructura se diseñó bajo un enfoque perimetral escalable (*Future-Proof*):
* **Análisis de Tráfico Complejo:** Durante el Módulo 3, el sistema ejecutará de forma simultánea herramientas de inspección profunda como **Wireshark** y navegadores web pesados. Un aprovisionamiento elevado previene la pérdida de paquetes (*packet dropping*) en los buffers virtuales durante capturas masivas.
* **Soporte Concurrentes y Forense:** En fases avanzadas de mitigación de amenazas (como Ransomware), se requerirá simular ataques dirigidos y levantar procesos analíticos concurrentes. Disponer de 11 vCPUs garantiza que el procesador físico segmente los hilos de ejecución sin sufrir bloqueos (*freezes*) destructivos.

### Paso 3: Despliegue del Sistema Operativo Invitado (Guest)
1. Definición de las credenciales iniciales automatizadas mediante el usuario genérico por defecto `vboxuser` [cite: 2].
2. Ejecución y carga del instalador nativo de Windows 11 dentro de la ventana del guest [cite: 2].
3. Monitoreo de la descompresión y copia de archivos del sistema operativo hasta verificar de manera exitosa el 100% de la instalación y el primer inicio de sesión al escritorio [cite: 2].

<!-- REEMPLAZA ESTA RUTA POR TU CAPTURA DE WINDOWS FUNCIONANDO -->
![Evidencia 3 - Escritorio Windows 11 Activo](img/escritorio.png)

---

## 3. Análisis Profundo: Configuración NAT y su Importancia

> **¿Para qué sirve el modo NAT en el Laboratorio?**  
> El modo **NAT (Network Address Translation)** actúa como un firewall unidireccional y un traductor de direcciones automatizado [cite: 2]. Permite que la máquina virtual acceda de forma segura a Internet para descargar firmas de antivirus, herramientas de diagnóstico (como Sysinternals o Wireshark) y parches de actualización utilizando la interfaz física del host, sin exponer la red local interna de nuestro hogar [cite: 1, 2].

### Ventajas de NAT implementadas en el Laboratorio:
* **Acceso controlado a Internet:** La VM puede iniciar conexiones hacia el exterior, pero ningún atacante o equipo externo desde Internet puede iniciar una conexión directa hacia el guest [cite: 2].
* **Aislamiento de la Red Física (LAN):** La máquina virtual recibe una dirección IP privada estandarizada en el rango `10.0.2.x` (específicamente la dirección `10.0.2.15` asignada dinámicamente) [cite: 2]. Esto evita que el entorno de pruebas interactúe de forma maliciosa con el router del hogar u otros dispositivos domésticos conectados a la misma red de la casa [cite: 1, 2].
* **Mitigación de riesgos:** En caso de que se ejecute una muestra sospechosa o se explote una vulnerabilidad dentro de la VM, los ataques de escaneo lateral quedan completamente bloqueados en la capa del hipervisor [cite: 1].

### Verificación mediante IPConfig (Validación de Red):
Al abrir la consola de comandos (`cmd`) dentro de la máquina virtual y ejecutar el comando `ipconfig`, se auditaron los siguientes parámetros del adaptador Ethernet virtual [cite: 2]:
* **Dirección IPv4 asignada por VirtualBox:** `10.0.2.15` [cite: 2]
* **Máscara de subred:** `255.255.255.0` [cite: 2]
* **Puerta de enlace predeterminada (Gateway virtual):** `10.0.2.2` [cite: 2]

<!-- REEMPLAZA ESTA RUTA POR TU CAPTURA DE IPCONFIG REAL -->
![Evidencia 4 - Comando IPConfig NAT](img/ipconfig.png)

---

## 4. Administración de Usuarios e Identidades (Hardening)

Se realizó la auditoría del sistema mediante la consola de *Administración de equipos -> Usuarios locales* para segmentar las identidades bajo las mejores prácticas internacionales de seguridad de la información [cite: 2]:
* **Cuenta de uso diario sin privilegios:** Representada por el perfil `vboxuser`, configurado como usuario estándar para evitar ejecuciones automáticas de comandos dañinos globales [cite: 2].
* **Cuenta Administrador:** Mantenida con restricciones claras de acceso y credenciales de alta complejidad, asegurando que cualquier cambio del sistema requiera autorización inequívoca mediante el Control de Cuentas de Usuario (UAC) [cite: 1, 2].
* Se desmarcaron casillas de riesgo heredado en las propiedades para mantener un control granular sobre la caducidad y el estado de habilitación de los perfiles locales [cite: 2].

<!-- REEMPLAZA ESTA RUTA POR TU CAPTURA DE USUARIOS REAL -->
![Evidencia 5 - Administración de Usuarios](img/usuarios.png)

---

## 5. Conclusión y Buenas Prácticas
La implementación de Windows 11 sobre Oracle VirtualBox permitió construir un laboratorio seguro, resiliente y funcional [cite: 2]. El uso de la tecnología NAT proporcionó acceso controlado a Internet manteniendo el aislamiento estricto respecto de la red física, característica fundamental para la realización de prácticas avanzadas de ciberseguridad [cite: 2]. Como práctica continua obligatoria, la generación de instantáneas (*Snapshots*) completará la resiliencia operativa de este entorno seguro [cite: 2].
