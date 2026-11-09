# Chronosense.ai: Arquitectura de Privacidad y Cifrado End-to-End (E2EE)

> **Documento de Ingeniería y Compliance Técnico**  
> **Versión:** 1.0 (2026)  
> **Clasificación:** Confidencial / Executive Briefing  

---

### 1. Principio rector: *Privacy by Design*
En el desarrollo de ecosistemas de IA ambiental y salud cognitiva, la exposición de datos biométricos, flujos de vídeo POV y geolocalización representa el riesgo operativo y legal más crítico. Chronosense.ai adopta una arquitectura de **Cifrado de Conocimiento Cero (Zero-Knowledge Architecture)**, garantizando que ni los operadores de la plataforma ni terceros puedan acceder al contenido desprotegido de los pacientes y sus familias.

---

### 2. Flujo de Cifrado de Datos en Tres Capas

#### Capa A: En el Dispositivo (Edge Device & Wearables)
* **Generación y Cifrado Local:** Los datos sensibles capturados por las gafas inteligentes (vídeos de legado, resúmenes de audio) o por la pulsera GPS se procesan mediante modelos multimodales ligeros en el propio dispositivo (*Edge AI*).
* **Cifrado AES-256:** Antes de cualquier transmisión a la nube, los archivos multimedia y metadatos se encriptan localmente utilizando el estándar de cifrado simétrico **AES-256** (Advanced Encryption Standard).
* **Borrado de Memoria Temporal:** Una vez completada la sincronización cifrada con el servidor, los archivos almacenados en la memoria caché local del wearable se purgan de forma instantánea para evitar vulnerabilidades físicas en caso de pérdida o robo del dispositivo.

#### Capa B: En Tránsito (In-Transit Protection)
* Toda la comunicación entre los dispositivos del paciente, la red de la pulsera y los servidores en la nube se realiza exclusivamente a través de canales seguros bajo el protocolo **TLS 1.3 (Transport Layer Security)**, impidiendo ataques de interceptación (*Man-in-the-Middle*).

#### Capa C: En Reposo (Cloud Storage & KMS)
* **Almacenamiento Aislado:** Los datos cifrados residen en infraestructura cloud certificada (como Google Cloud Platform o AWS) bajo clóset de datos geolocalizado en la Unión Europea (`europe-west1`), cumpliendo estrictamente con los mandatos de soberanía de datos del **GDPR**.
* **Gestión de Claves (KMS - Key Management Service):** Las claves criptográficas maestras para descifrar el *Legacy Vault* y los historiales de salud están gestionadas mediante sistemas de cifrado controlado por el usuario (CMEK). Las claves de descifrado residen exclusivamente en el dispositivo de confianza del tutor legal, lo que significa que el almacenamiento en la nube es matemáticamente ilegible sin la autorización directa de la familia.

---

### 3. Seguridad y Privacidad en el Modo de Rescate QR (Community Rescue)
Para equilibrar la velocidad de rescate en la calle con la privacidad absoluta del paciente, el sistema de códigos QR opera bajo un esquema de **Tokens Dinámicos y Desacoplados**:

* **Identificadores No Sensibles:** La placa metálica de la pulsera **nunca** muestra nombres, direcciones ni datos médicos legibles; únicamente incorpora un código QR vinculado a un UUID aleatorio (ej: `chronosense.ai/r/8f4c-99a1`).
* **Acceso Condicional y Temporal:** Cuando un transeúnte escanea el QR en una situación de emergencia:
  1. El servidor verifica la petición de forma anonimizada.
  2. Activa de manera temporal (sesión efímera de 15 minutos) el perfil de emergencia mínimo indispensable: el vídeo de identidad del paciente y el teléfono de contacto cifrado del cuidador.
  3. La geolocalización GPS exacta **no se expone públicamente en la web**, sino que se transmite mediante una pasarela segura directamente al dispositivo del familiar autorizado que recibe la alerta SOS.

---

### 4. Cumplimiento Normativo (Compliance Framework)

| Normativa / Estándar | Estado de Implementación en Chronosense.ai |
| :--- | :--- |
| **HIPAA (Health Insurance Portability and Accountability Act)** | Cumplimiento mediante la formalización de acuerdos BAA (*Business Associate Agreement*) con los proveedores de servicios cloud y aislamiento estricto de los Datos de Salud Protegidos (PHI). |
| **GDPR (Reglamento General de Protección de Datos - UE)** | Incorporación nativa del *Derecho al Olvido* (borrado automatizado e irreversible de todos los registros de un usuario a petición del tutor legal) y registro de consentimiento explícito granular. |
| **Aislamiento de Modelos de IA** | Compromiso contractual y técnico de que los datos biométricos, la voz de los familiares y los vídeos de legado **jamás** se utilizan para entrenar modelos públicos de inteligencia artificial de terceros. |