# Redireccionador de QR Dinámico — RISE

Landing ultra simple desplegada en Vercel. El QR que entregas al cliente **nunca cambia** y este repositorio **no requiere más ediciones** después de la configuración inicial.

## Cómo funciona

1. El cliente escanea un QR fijo que apunta a tu URL de Vercel (ej. `https://rise-redirect.vercel.app`).
2. Vercel sirve `index.html`, que redirige al instante al canal permanente `preview` de Expo.
3. Expo resuelve automáticamente la versión más reciente publicada en ese canal.

Gracias a apuntar a `/channels/preview` en lugar de un update ID concreto, la redirección siempre lleva al último avance sin tocar código ni redesplegar Vercel.

```
QR fijo → Vercel → expo.dev/.../channels/preview → último EAS Update
```

## Flujo de trabajo (100% automático)

Este despliegue es **definitivo**. Configúralo una vez y olvídate de este repo.

### Configuración inicial (una sola vez)

1. Despliega este repositorio en [Vercel](https://vercel.com) (sitio estático, sin build).
2. Genera el QR eterno apuntando a la URL de Vercel (ver sección inferior).
3. Entrega el QR al cliente.

### Cada nuevo avance (solo desde tu terminal)

Desde el proyecto Expo, publica al canal `preview`:

```bash
eas update --branch preview
```

Eso es todo. El QR y Vercel siguen igual; Expo actualiza el contenido del canal en segundo plano y el cliente recibe la versión más reciente al escanear.

## Desplegar en Vercel

1. Sube este repositorio a GitHub, GitLab o Bitbucket.
2. En [vercel.com](https://vercel.com), importa el proyecto.
3. Vercel detectará el sitio estático automáticamente (no requiere framework ni build).
4. Copia la URL de producción (ej. `https://tu-proyecto.vercel.app`).

## Generar el QR eterno (una sola vez)

El QR debe apuntar **siempre** a la URL de Vercel, nunca directamente a Expo.

### Opción A — Herramienta online (recomendada)

1. Ve a [qr-code-generator.com](https://www.qr-code-generator.com/) o [goqr.me](https://goqr.me/).
2. Elige tipo **URL**.
3. Pega la URL de Vercel (ej. `https://tu-proyecto.vercel.app`).
4. Descarga el PNG o SVG en alta resolución.
5. Entrega ese archivo al cliente. No hace falta regenerarlo nunca más.

### Opción B — CLI con `qrencode`

```bash
# Instalar (Ubuntu/Debian)
sudo apt install qrencode

# Generar QR
qrencode -o rise-qr.png "https://tu-proyecto.vercel.app"
```

### Opción C — Node.js con `qrcode`

```bash
npx qrcode "https://tu-proyecto.vercel.app" -o rise-qr.png
```

## Checklist por avance

- [ ] `eas update --branch preview` desde el proyecto Expo
- [ ] Verificar que la app carga la versión nueva (escaneo de prueba)
- [ ] **No** tocar este repositorio
- [ ] **No** regenerar el QR
# qr-redirector
