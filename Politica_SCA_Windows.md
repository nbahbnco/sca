## Política SCA Windows basada en ISO 27001 / ISO 27002

Este documento recoge las normas técnicas recomendadas para la política de Security Configuration Assessment (SCA) aplicada a equipos Windows, tomando como referencia los controles de **ISO/IEC 27001** y las buenas prácticas del apéndice de **ISO/IEC 27002**.

Las columnas **Implementado** y **No se implementará** permiten marcar el estado de cada norma.  
En la columna **Implementado** ya se han marcado con `X` aquellos controles que están cubiertos por la política `basic_win.yml` actual.

---

## 1. Identificación y autenticación (contraseñas y cuentas)


| ID   | Norma / configuración                                                         | Descripción breve                                                                  | ISO 27001 / 27002 (aprox.)         | Implementado | No se implementará |
| ---- | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------- | ------------ | ------------------ |
| N-01 | Historial de contraseñas ≥ 24                                                 | Mantener historial para impedir reutilizar contraseñas recientes.                  | A.5.17, A.8.2, A.8.3 / 27002-8.2.1 | X            |                    |
| N-02 | Antigüedad mínima de contraseña ≥ 1 día                                       | Impedir cambios sucesivos inmediatos para saltarse el historial de contraseñas.    | A.5.17, A.8.2 / 27002-8.2.1        | X            |                    |
| N-03 | Longitud mínima de contraseña ≥ 14 caracteres                                 | Exigir contraseñas/frases de contraseña largas y robustas.                         | A.5.17, A.8.2 / 27002-8.2.1        | X            |                    |
| N-04 | Permitir longitud mínima extendida de contraseña (RelaxMinimumPasswordLength) | Permitir requerir contraseñas aún más largas (más de 14 caracteres).               | A.5.17 / 27002-8.2.1               | X            |                    |
| N-05 | Complejidad de contraseñas habilitada                                         | Obligar combinación de tipos de caracteres (mayús, minús, números, símbolos).      | A.5.17 / 27002-8.2.1               |              |                    |
| N-06 | Antigüedad máxima de contraseña definida (p.ej. ≤ 365 días, no ilimitada)     | Forzar el cambio periódico de credenciales de cuentas críticas.                    | A.5.17 / 27002-8.2.1               |              | x                  |
| N-07 | No almacenar contraseñas con cifrado reversible                               | Evitar almacenamiento reversible de contraseñas en el sistema.                     | A.5.17, A.8.2 / 27002-8.2.1        |              |                    |
| N-08 | Bloqueo de cuenta para usuario Administrator                                  | Permitir que la cuenta Administrador se bloquee ante intentos fallidos reiterados. | A.8.2, A.8.3 / 27002-8.2.2         |              |                    |
| N-09 | Renombrar / deshabilitar cuenta Administrator y deshabilitar Guest            | Reducir la superficie de ataque de cuentas conocidas por defecto.                  | A.8.2, A.8.3 / 27002-8.2.2         |              |                    |
| N-10 | Revisar pertenencia a grupos locales privilegiados                            | Solo cuentas autorizadas en `Administrators`, `Remote Desktop Users`, etc.         | A.5.18, A.8.2 / 27002-8.2.2        |              |                    |


---

## 2. Bloqueo de cuentas y sesiones


| ID   | Norma / configuración                                          | Descripción breve                                                                             | ISO 27001 / 27002 (aprox.) | Implementado | No se implementará |
| ---- | -------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | -------------------------- | ------------ | ------------------ |
| N-11 | Duración del bloqueo de cuenta ≥ 10–15 minutos                 | Tiempo mínimo que una cuenta permanece bloqueada tras superar el umbral de intentos fallidos. | A.8.2, A.8.3 / 27002-8.2.3 | X            |                    |
| N-12 | Umbral de bloqueo de cuenta (p.ej. ≤ 5–10 intentos, pero no 0) | Número máximo de intentos fallidos antes de bloquear la cuenta.                               | A.8.2, A.8.3 / 27002-8.2.3 | X            |                    |
| N-13 | Restablecer contador de bloqueo tras ≥ 10–15 minutos           | Tiempo tras el cual se reinicia el contador de intentos fallidos.                             | A.8.2, A.8.3 / 27002-8.2.3 | X            |                    |
| N-14 | Límite de inactividad del equipo ≤ 900s (no 0)                 | Bloqueo automático de sesión tras un periodo de inactividad.                                  | A.8.2, A.8.3 / 27002-8.2.8 | X            |                    |
| N-15 | Número de inicios de sesión anteriores en caché ≤ 4            | Reducir la información de logon almacenada localmente para escenarios sin DC.                 | A.8.2, A.8.3 / 27002-8.2.2 | X            |                    |
| N-16 | Requerir `Ctrl+Alt+Supr` para iniciar sesión                   | Reducir riesgo de falsificación de pantallas de logon.                                        | A.8.2 / 27002-8.2.2        |              |                    |
| N-17 | Ocultar último usuario que inició sesión                       | Evitar filtrado de información de cuentas válidas.                                            | A.8.2, A.8.3 / 27002-8.2.2 |              |                    |


---

## 3. Mensajes legales y concienciación en el logon


| ID   | Norma / configuración                              | Descripción breve                                            | ISO 27001 / 27002 (aprox.)               | Implementado | No se implementará |
| ---- | -------------------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- | ------------ | ------------------ |
| N-18 | Texto de mensaje de inicio de sesión corporativo   | Mensaje legal / de uso aceptable al intentar iniciar sesión. | A.5.1, A.5.2, A.5.37 / 27002-5.1.1, 5.37 | X            |                    |
| N-19 | Título del mensaje de inicio de sesión corporativo | Título coherente con política y avisos legales.              | A.5.1, A.5.2 / 27002-5.1.1               | X            |                    |


---

## 4. Gestión de parches y actualizaciones (Windows Update)


| ID   | Norma / configuración                                                               | Descripción breve                                                                        | ISO 27001 / 27002 (aprox.)            | Implementado | No se implementará |
| ---- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------- | ------------ | ------------------ |
| N-20 | Actualizaciones automáticas habilitadas (AUOptions = 4 u otra política corporativa) | Asegurar que el sistema descarga e instala automáticamente actualizaciones de seguridad. | A.8.8, A.8.9, A.8.10 / 27002-8.8–8.10 | X            |                    |
| N-21 | Uso de WSUS/Intune u otro gestor centralizado (si aplica)                           | Control central sobre aprobación e instalación de parches.                               | A.5.36, A.8.9 / 27002-5.36, 8.9       |              |                    |
| N-22 | Verificación de ausencia de parches críticos pendientes durante largos periodos     | Comprobaciones periódicas de cumplimiento de parches de seguridad.                       | A.8.8, A.8.9 / 27002-8.8, 8.9         |              |                    |
| N-23 | Política de reinicio tras instalación de parches                                    | Definir y comprobar reinicios programados para completar la instalación.                 | A.5.36, A.8.9 / 27002-5.36, 8.9       |              |                    |


---

## 5. Registro y monitorización


| ID   | Norma / configuración                                                               | Descripción breve                                                          | ISO 27001 / 27002 (aprox.)        | Implementado | No se implementará |
| ---- | ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | --------------------------------- | ------------ | ------------------ |
| N-24 | Auditoría de eventos de seguridad activada (logon/logoff, cambios de cuentas, etc.) | Registrar eventos clave para trazabilidad y detección de incidentes.       | A.8.15, A.8.16 / 27002-8.15, 8.16 |              |                    |
| N-25 | Tamaño mínimo y retención de Security Event Log                                     | Evitar pérdida prematura de eventos relevantes.                            | A.8.15 / 27002-8.15               |              |                    |
| N-26 | Protección de los logs (permisos, no borrado no autorizado)                         | Restringir modificación y borrado de registros.                            | A.8.15, A.8.16 / 27002-8.15, 8.16 |              |                    |
| N-27 | Sincronización de hora (NTP)                                                        | Hora del sistema alineada con fuentes confiables para correlación de logs. | A.8.15, A.8.16 / 27002-8.15       |              |                    |


---

## 6. Configuración de energía y arranque


| ID   | Norma / configuración                  | Descripción breve                                                                                                     | ISO 27001 / 27002 (aprox.)        | Implementado | No se implementará |
| ---- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------- | ------------ | ------------------ |
| N-28 | Desactivar Hybrid Sleep / Fast Startup | Evitar que el estado del sistema se almacene de manera que debilite controles de cifrado o autenticación en arranque. | A.8.10, A.8.11 / 27002-8.10, 8.11 | X            |                    |


---

## 7. Protección del endpoint y antimalware


| ID   | Norma / configuración                                        | Descripción breve                                             | ISO 27001 / 27002 (aprox.)    | Implementado | No se implementará |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------- | ----------------------------- | ------------ | ------------------ |
| N-29 | Antimalware instalado, activo y actualizado                  | Comprobación de la presencia y estado del motor AV/EDR.       | A.8.7, A.8.8 / 27002-8.7, 8.8 |              |                    |
| N-30 | Escaneos programados y protección en tiempo real             | Verificar que hay análisis recurrentes y protección continua. | A.8.7 / 27002-8.7             |              |                    |
| N-31 | Control de aplicaciones (AppLocker/WDAC) en equipos críticos | Restringir ejecución a aplicaciones autorizadas.              | A.8.7, A.8.9 / 27002-8.7, 8.9 |              |                    |


---

## 8. Red y firewall


| ID   | Norma / configuración                                | Descripción breve                                             | ISO 27001 / 27002 (aprox.)        | Implementado | No se implementará |
| ---- | ---------------------------------------------------- | ------------------------------------------------------------- | --------------------------------- | ------------ | ------------------ |
| N-32 | Firewall de Windows habilitado en todos los perfiles | Garantizar filtrado de tráfico entrante/saliente por defecto. | A.8.20, A.8.21 / 27002-8.20, 8.21 |              |                    |
| N-33 | Solo puertos/servicios necesarios permitidos         | Reglas de firewall restrictivas según rol (servidor/puesto).  | A.8.20, A.8.21 / 27002-8.20, 8.21 |              |                    |
| N-34 | Deshabilitar SMBv1                                   | Eliminar protocolo antiguo inseguro.                          | A.8.21, A.8.8 / 27002-8.21, 8.8   |              |                    |
| N-35 | Desactivar impresión sobre HTTP si no se necesita    | Reducir superficie de ataque vía HTTP printing.               | A.8.21 / 27002-8.21               |              |                    |


---

## 9. Acceso remoto y RDP


| ID   | Norma / configuración                                       | Descripción breve                                   | ISO 27001 / 27002 (aprox.)        | Implementado | No se implementará |
| ---- | ----------------------------------------------------------- | --------------------------------------------------- | --------------------------------- | ------------ | ------------------ |
| N-36 | Deshabilitar RDP si no se usa                               | Eliminar servicio de escritorio remoto innecesario. | A.8.20, A.8.21 / 27002-8.20, 8.21 |              |                    |
| N-37 | Si RDP se usa, forzar NLA y restringir a grupos específicos | Asegurar autenticación previa y mínima exposición.  | A.8.2, A.8.20 / 27002-8.2.2, 8.20 |              |                    |
| N-38 | Limitar intentos de conexión RDP y orígenes (firewall/VPN)  | Reducir ataques de fuerza bruta sobre RDP.          | A.8.20, A.8.21 / 27002-8.20, 8.21 |              |                    |


---

## 10. Dispositivos, almacenamiento y cifrado


| ID   | Norma / configuración                                         | Descripción breve                                                         | ISO 27001 / 27002 (aprox.)        | Implementado | No se implementará |
| ---- | ------------------------------------------------------------- | ------------------------------------------------------------------------- | --------------------------------- | ------------ | ------------------ |
| N-39 | BitLocker habilitado en unidades de sistema y datos           | Cifrar datos en reposo de equipos portátiles y estaciones críticas.       | A.8.10, A.8.11 / 27002-8.10, 8.11 |              |                    |
| N-40 | Política de claves de recuperación BitLocker                  | Definir dónde se almacenan y cómo se protegen las claves de recuperación. | A.8.11, A.5.32 / 27002-8.11, 5.32 |              |                    |
| N-41 | Control de dispositivos USB (lectura sola o lista blanca)     | Limitar copia no controlada de información a medios extraíbles.           | A.8.9, A.8.12 / 27002-8.9, 8.12   |              |                    |
| N-42 | Deshabilitar unidades ópticas / antiguos medios si no se usan | Reducir vectores de fuga o entrada de malware.                            | A.8.9, A.8.12 / 27002-8.9, 8.12   |              |                    |


---

## 11. Hardening del sistema y explotación


| ID   | Norma / configuración                                                      | Descripción breve                                                      | ISO 27001 / 27002 (aprox.)      | Implementado | No se implementará |
| ---- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------- | ------------------------------- | ------------ | ------------------ |
| N-43 | Exploit Protection (DEP, ASLR, etc.) con perfil corporativo                | Habilitar mitigaciones de explotación a nivel de sistema y aplicación. | A.8.7, A.8.8 / 27002-8.7, 8.8   |              |                    |
| N-44 | Políticas de ejecución de PowerShell restringidas (RemoteSigned/AllSigned) | Limitar ejecución de scripts no firmados y registrar su uso.           | A.8.7, A.8.15 / 27002-8.7, 8.15 |              |                    |
| N-45 | Habilitar Credential Guard / LSA Protection cuando sea posible             | Proteger credenciales almacenadas en memoria.                          | A.8.7, A.8.11 / 27002-8.7, 8.11 |              |                    |
| N-46 | Deshabilitar servicios y funciones no utilizados (roles, características)  | Reducir superficie de ataque eliminando componentes innecesarios.      | A.8.9, A.8.21 / 27002-8.9, 8.21 |              |                    |


---

## 12. Navegación, aplicaciones y telemetría


| ID   | Norma / configuración                                                         | Descripción breve                                                                              | ISO 27001 / 27002 (aprox.)        | Implementado | No se implementará |
| ---- | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------- | ------------ | ------------------ |
| N-47 | Políticas de navegador (bloqueo plugins inseguros, sitios restringidos, etc.) | Controlar comportamientos de navegación para reducir exposición a malware / fuga de datos.     | A.8.20, A.8.21 / 27002-8.20, 8.21 |              |                    |
| N-48 | Restringir instalación de software a administradores                          | Evitar que usuarios estándar instalen software no autorizado.                                  | A.8.9, A.5.36 / 27002-8.9, 5.36   |              |                    |
| N-49 | Deshabilitar programas de experiencia del cliente / telemetría no necesaria   | Reducir envío de datos a terceros (Microsoft, etc.) no alineado con la política de privacidad. | A.5.29, A.8.12 / 27002-5.29, 8.12 |              |                    |


