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
2. <img width="639" height="509" alt="Screenshot_4" src="https://github.com/user-attachments/assets/2b32fefc-62ef-4ec8-bd3f-7d85c1ae4986" />
<img width="643" height="506" alt="Screenshot_2" src="https://github.com/user-attachments/assets/7d4edf00-0a69-473f-bd2d-e064617a525e" />

3. Aceptación de los términos de la Licencia de Usuario Final (GPL v3) [cite: 2].
4. <img width="655" height="531" alt="Screenshot_1" src="https://github.com/user-attachments/assets/54d81e4e-b7f0-43e2-9378-1e1c0c7f6c5b" />

5. Configuración personalizada de características (*Custom Setup*) incluyendo soporte USB, componentes de red esenciales y bindings de Python [cite: 2].
6. <img width="647" height="508" alt="Screenshot_3" src="https://github.com/user-attachments/assets/2da7e9a0-bc21-4aaa-8d7e-3f59749f698b" />


7. Aceptación del aviso de desconexión temporal de red física necesaria para compilar las interfaces virtuales del hipervisor [cite: 2].

8. <img width="639" height="509" alt="Screenshot_4" src="https://github.com/user-attachments/assets/33cbf2b7-e646-40e0-b474-593452a8f31e" />

<img width="638" height="515" alt="Screenshot_5" src="https://github.com/user-attachments/assets/ec90be83-9b5b-445f-81f1-c7926ef6850a" />

<img width="636" height="517" alt="Screenshot_6" src="https://github.com/user-attachments/assets/03e26c7d-7cdf-438a-888f-87ccdf39e305" />

<img width="638" height="516" alt="Screenshot_7" src="https://github.com/user-attachments/assets/6e65a605-1f21-4b3f-9589-2e265b4f503c" />

<img width="642" height="503" alt="Screenshot_8" src="https://github.com/user-attachments/assets/7833438b-520d-40c5-9f42-5ed7cb06eb7f" />

<img width="671" height="511" alt="Screenshot_9" src="https://github.com/user-attachments/assets/24260c4c-c7c1-419e-bd54-fb720b7274a1" />



### Paso 2: Creación y Aprovisionamiento del Hardware Virtual
1. Inicialización del Administrator de VirtualBox y selección de la opción **"Nueva"** [cite: 2].

2. <img width="964" height="923" alt="Screenshot_10" src="https://github.com/user-attachments/assets/83225b38-343a-4783-9967-99d720bd3642" />

3. Asignación del nombre unívoco de la máquina virtual: `PCII` [cite: 2].<img width="1171" height="792" alt="Screenshot_13" src="https://github.com/user-attachments/assets/42d4090a-c1cf-403b-b87d-429821fd89be" />


4. Montaje del archivo de imagen de disco óptico (ISO) oficial de `Windows 11 Client x64` [cite: 2].<img width="996" height="489" alt="Screenshot_14" src="https://github.com/user-attachments/assets/3b2ebeb6-3737-44b7-8039-0642f29b250f" />

5. Habilitación de la casilla *"Proceed with Unattended Installation"* para automatizar los parámetros básicos [cite: 2].<img width="996" height="489" alt="Screenshot_14" src="https://github.com/user-attachments/assets/d311a96a-a8f5-4d81-97e6-5215b72514e3" />

6. **Asignación de Recursos Críticos:** Provisión de hardware asignando **15808 MB de Memoria Base (aprox. 15 GB RAM)** y **11 núcleos de procesamiento CPU**, activando el entorno de firmware **EFI** para cumplir con las exigencias nativas del sistema operativo moderno [cite: 2].<img width="1050" height="907" alt="Screenshot_16" src="https://github.com/user-attachments/assets/0ad43e2a-f873-4035-9887-69b63971774e" />


<img width="1003" height="926" alt="Screenshot_17" src="https://github.com/user-attachments/assets/8a0c915f-bc76-4783-bdc5-92795b117aa0" />


### Nota de Arquitectura (Justificación de Recursos)
Se determinó una asignación masiva de **15,808 MB de RAM** y **11 núcleos de vCPU** debido a que este entorno no se limitará a ser una máquina cliente de uso simple [cite: 2]. Esta infraestructura se diseñó bajo un enfoque perimetral escalable (*Future-Proof*):
* **Análisis de Tráfico Complejo:** Durante el Módulo 3, el sistema ejecutará de forma simultánea herramientas de inspección profunda como **Wireshark** y navegadores web pesados. Un aprovisionamiento elevado previene la pérdida de paquetes (*packet dropping*) en los buffers virtuales durante capturas masivas.
* **Soporte Concurrentes y Forense:** En fases avanzadas de mitigación de amenazas (como Ransomware), se requerirá simular ataques dirigidos y levantar procesos analíticos concurrentes. Disponer de 11 vCPUs garantiza que el procesador físico segmente los hilos de ejecución sin sufrir bloqueos (*freezes*) destructivos.

### Paso 3: Despliegue del Sistema Operativo Invitado (Guest)Attach files by dragging & dropping, selecting or pasting them.

1. Definición de las credenciales iniciales automatizadas mediante el usuario genérico por defecto `vboxuser` [cite: 2].<img width="1016" height="742" alt="Screenshot_15" src="https://github.com/user-attachments/assets/7c993060-93a6-4418-b10a-dc1c0f5fdc1e" />

2. Ejecución y carga del instalador nativo de Windows 11 dentro de la ventana del guest [cite: 2].<img width="1275" height="870" alt="Screenshot_18" src="https://github.com/user-attachments/assets/cfc94d0e-e6a4-4ec7-b576-0dc79c4ebe11" />

3. Monitoreo de la descompresión y copia de archivos del sistema operativo hasta verificar de manera exitosa el 100% de la instalación y el primer inicio de sesión al escritorio [cite: 2].<img width="1498" height="949" alt="Screenshot_19" src="https://github.com/user-attachments/assets/6845b38d-c09d-497b-a7fc-9d4ea7b66d25" />

4. Evidenciamos la instalacion correcta de windows.
5. <img width="1364" height="888" alt="Screenshot_20" src="https://github.com/user-attachments/assets/e28d3c18-bda3-4d33-9415-55d75eae5ae9" />


## 3. Análisis Profundo: Configuración NAT y su Importancia

> **¿Para qué sirve el modo NAT en el Laboratorio?**  
> El modo **NAT (Network Address Translation)** actúa como un firewall unidireccional y un traductor de direcciones automatizado [cite: 2]<img width="1171" height="792" alt="Screenshot_13" src="https://github.com/user-attachments/assets/8ef1744d-36db-42bd-9631-409972a6354b" />
. Permite que la máquina virtual acceda de forma segura a Internet para descargar firmas de antivirus, herramientas de diagnóstico (como Sysinternals o Wireshark) y parches de actualización utilizando la interfaz física del host, sin exponer la red local interna de nuestro hogar [cite: 1, 2].

### Ventajas de NAT implementadas en el Laboratorio:
* **Acceso controlado a Internet:** La VM puede iniciar conexiones hacia el exterior, pero ningún atacante o equipo externo desde Internet puede iniciar una conexión directa hacia el guest [cite: 2].
* **Aislamiento de la Red Física (LAN):** La máquina virtual recibe una dirección IP privada estandarizada en el rango `10.0.2.x` (específicamente la dirección `10.0.2.15` asignada dinámicamente) [cite: 2]. Esto evita que el entorno de pruebas interactúe de forma maliciosa con el router del hogar u otros dispositivos domésticos conectados a la misma red de la casa [cite: 1, 2].<img width="1360" height="881" alt="Screenshot_21" src="https://github.com/user-attachments/assets/6429f193-ee71-46a5-af54-69dcdd24c472" />

* **Mitigación de riesgos:** En caso de que se ejecute una muestra sospechosa o se explote una vulnerabilidad dentro de la VM, los ataques de escaneo lateral quedan completamente bloqueados en la capa del hipervisor [cite: 1].

### Verificación mediante IPConfig (Validación de Red):
Al abrir la consola de comandos (`cmd`) dentro de la máquina virtual y ejecutar el comando `ipconfig`, se auditaron los siguientes parámetros del adaptador Ethernet virtual [cite: 2]:
* **Dirección IPv4 asignada por VirtualBox:** `10.0.2.15` [cite: 2]<img width="1360" height="881" alt="Screenshot_21" src="https://github.com/user-attachments/assets/02a79f67-461a-4abd-9273-a08172c032db" />

* **Máscara de subred:** `255.255.255.0` [cite: 2]
* **Puerta de enlace predeterminada (Gateway virtual):** `10.0.2.2` [cite: 2]

![Uploading Screenshot_21.png…]()


---

## 4. Administración de Usuarios e Identidades (Hardening)

Se realizó la auditoría del sistema mediante la consola de *Administración de equipos -> Usuarios locales* para segmentar las identidades bajo las mejores prácticas internacionales de seguridad de la información [cite: 2]:
* **Cuenta de uso diario sin privilegios:** Representada por el perfil `vboxuser`, configurado como usuario estándar para evitar ejecuciones automáticas de comandos dañinos globales [cite: 2].
* **Cuenta Administrador:** Mantenida con restricciones claras de acceso y credenciales de alta complejidad, asegurando que cualquier cambio del sistema requiera autorización inequívoca mediante el Control de Cuentas de Usuario (UAC) [cite: 1, 2].<img width="1754" height="877" alt="Screenshot_22" src="https://github.com/user-attachments/assets/6994e573-1e4f-404c-a6ee-be929a5ed5c3" />

* Se desmarcaron casillas de riesgo heredado en las propiedades para mantener un control granular sobre la caducidad y el estado de habilitación de los perfiles locales [cite: 2].
<img width="1782" height="818" alt="Screenshot_23" src="https://github.com/user-attachments/assets/9fa8a25c-fac0-4e01-9cc3-f56a0338f3df" />

<img width="1784" height="841" alt="Screenshot_24" src="https://github.com/user-attachments/assets/4971b805-b91e-490d-8eb1-c13d3f0022fc" />


---

## 5. Conclusión y Buenas Prácticas
La implementación de Windows 11 sobre Oracle VirtualBox permitió construir un laboratorio seguro, resiliente y funcional [cite: 2]. El uso de la tecnología NAT proporcionó acceso controlado a Internet manteniendo el aislamiento estricto respecto de la red física, característica fundamental para la realización de prácticas avanzadas de ciberseguridad [cite: 2]. Como práctica continua obligatoria, la generación de instantáneas (*Snapshots*) completará la resiliencia operativa de este entorno seguro [cite: 2].
<img width="1027" height="884" alt="image" src="https://github.com/user-attachments/assets/6641e79b-f29e-486a-9fe4-22c38cc99076" />

