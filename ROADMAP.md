# 🗺️ Roadmap — Sitio Web JAL Comuna 11 (Medellín)

> Documento de planeación del proyecto. Proyecto **real** para la Junta Administradora
> Local de la Comuna 11, desarrollado como **trabajo de servicio social**.

---

## 🎯 Principios del proyecto

- **Mantenerlo SIMPLE.** Es un trabajo de servicio social; debe ser fácil de mantener
  por quien lo reciba después. **Evitar bases de datos (MySQL)** siempre que se pueda.
- **Bajo mantenimiento.** Preferir soluciones que no requieran soporte técnico continuo.
- **Cumplir la ley.** Al manejar datos de ciudadanos (PQRS, certificados), respetar la
  **Ley 1581 de 2012 (Habeas Data)**: aviso de privacidad y consentimiento en los formularios.

---

## 🧰 Stack técnico

| Componente              | Tecnología                                   |
|-------------------------|----------------------------------------------|
| Frontend                | HTML + CSS + Bootstrap 5 + Font Awesome 6    |
| Backend (mínimo)        | PHP                                          |
| Hosting                 | InfinityFree (ya configurado)                |
| Dominio                 | Ya adquirido ✅                               |
| Envío de correos        | PHPMailer + SMTP externo (Gmail/Brevo)       |
| Generar PDF (certificado)| FPDF o Dompdf (librería PHP)                |
| Almacenamiento          | **Basado en archivos** (carpetas/JSON), NO MySQL |

> ⚠️ Nota sobre InfinityFree: bloquea la función `mail()` de PHP. Por eso se usa
> **PHPMailer con un SMTP externo** (ej. Gmail con "contraseña de aplicación").

---

## ✅ Estado actual (hecho)

- [x] `index.html` — Página de inicio (hero, accesos rápidos, resumen JAL, noticias, contacto)
- [x] `Significadojal.html` — La JAL (¿Qué es?, Funciones, Integrantes + organigrama, Planeación)
- [x] `pqrs.html` — Página con el formulario de PQRS (frontend)
- [x] Navbar y footer consistentes en todo el sitio
- [x] Corregido: íconos Font Awesome (`font-weight: 900` para `.fa-solid`)
- [x] Sitio base montado en InfinityFree

---

## 📋 Plan por sesiones

### 🟢 Sesión 1 — Pulir el sitio estático
- [ ] Crear página de **Transparencia** (Presupuesto, Normatividad)
- [ ] Poner **mapa real** de Google Maps en la sección Contacto
- [ ] Agregar **favicon** (ícono de la pestaña del navegador)
- [ ] Revisar enlaces del navbar/footer en los 3 archivos (incluido PQRS → `pqrs.html`)
- [ ] Aplicar la regla de íconos Font Awesome en los 3 archivos

### 🟢 Sesión 2 — PQRS al correo (SIN base de datos)
- [ ] Configurar **PHPMailer + SMTP** (ej. Gmail con contraseña de aplicación)
- [ ] Crear `enviar_pqrs.php` que reciba el formulario y envíe el correo
- [ ] Agregar **aviso de privacidad + casilla de consentimiento** (Ley 1581)
- [ ] Probar que las PQRS lleguen al correo oficial de la JAL
- [ ] **Alternativa aún más simple:** usar Formspree/EmailJS si se prefiere sin PHP

### 🟡 Sesión 3 — Publicar decretos / noticias (SIN base de datos)
- [ ] Estrategia basada en archivos: carpeta de PDFs + un archivo `noticias.json`
      (o HTML simple) que liste el contenido
- [ ] Que la web lea esa carpeta/archivo y muestre los documentos automáticamente
- [ ] (Opcional) Panel mínimo protegido con contraseña para subir archivos
      — evaluar si vale la pena o si se suben manual por FTP

### 🔴 Sesión 4 y 5 — Certificado de residencia
- [ ] Formulario de solicitud + **adjuntar factura de EPM** + consentimiento de datos
- [ ] Las solicitudes llegan **al correo** (no a base de datos)
- [ ] **Generación automática del PDF** del certificado (FPDF/Dompdf)
- [ ] Flujo: un **funcionario de la JAL verifica** la factura y aprueba → se envía el PDF
- [ ] ⚠️ La verificación con EPM es **manual** (EPM no tiene API pública; verificar
      automáticamente no es viable ni legal)

---

## ⚠️ Decisiones y advertencias importantes

1. **Certificado de residencia:** NO se puede verificar automáticamente contra EPM.
   El ciudadano adjunta su factura y una persona la revisa. El sistema automatiza la
   generación y el envío del PDF, pero la aprobación es humana.

2. **Sin base de datos:** se prioriza almacenamiento por archivos y envío por correo.
   Solo se introducirá MySQL si alguna función es imposible sin ella (se avisará antes).

3. **Protección de datos (Ley 1581 de 2012):** todos los formularios que recojan datos
   personales deben incluir aviso de privacidad y consentimiento explícito.

4. **Límites de InfinityFree:** hosting gratuito con límites de CPU/visitas y bloqueo de
   `mail()`. Suficiente para una JAL pequeña; considerar hosting pago si el sitio crece.

---

## 📁 Estructura de archivos actual

```
/
├── index.html            # Inicio
├── Significadojal.html   # La JAL (qué es, funciones, integrantes, planeación)
├── pqrs.html             # Formulario de PQRS
├── ROADMAP.md            # Este documento
└── IMAGES/
    └── logo.png          # Logo de la JAL
```

### Estructura prevista (a futuro)
```
├── transparencia.html    # Presupuesto y normatividad
├── certificado.html      # Solicitud de certificado de residencia
├── enviar_pqrs.php       # Script que envía las PQRS por correo
├── enviar_certificado.php# Script del certificado
├── /lib/                 # Librerías PHP (PHPMailer, FPDF/Dompdf)
└── /documentos/          # Decretos y archivos públicos (almacenamiento por archivos)
```

---

## 🎯 Para empezar la próxima sesión

1. Tener a mano el correo oficial donde llegarán las PQRS.
2. Decidir el SMTP (lo más fácil: Gmail con contraseña de aplicación — se explica en Sesión 2).
3. Confirmar acceso al panel de InfinityFree y al gestor de archivos (FTP / File Manager).

---

_Última actualización: 28 de octubre de 2026_
