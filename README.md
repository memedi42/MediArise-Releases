# MediArise — canal de distribución

Este repositorio **solo distribuye builds**. No contiene código fuente.

Aquí viven dos cosas y nada más:

- **`mediarise-update.json`** — la metadata que la app consulta para saber si
  existe una versión más reciente.
- **Releases** — cada una con su APK firmado, `mediarise-release-<versión>.apk`.

La app comprueba las actualizaciones de forma anónima: descarga ese JSON, y no
envía ningún dato ni requiere ninguna cuenta.

## Verificar un APK

Todas las builds están firmadas con la misma clave permanente. Su huella
pública es:

```
582a522a83548b02109298fa725de38f3e49cf16b85e1cbbad44a2d2410ecab8
```

Se puede comprobar sobre cualquier APK descargado de aquí:

```
apksigner verify --print-certs --verbose mediarise-release-<versión>.apk
```

Un APK que no presente esa huella no viene de este canal, y Android se
negaría a instalarlo encima de una instalación existente.

Cada release publica además el SHA-256 del archivo dentro de
`mediarise-update.json`; la app lo comprueba antes de abrir el instalador.

## Formato de `mediarise-update.json`

```json
{
  "schema": 1,
  "versionCode": 18,
  "versionName": "1.0.18",
  "apkUrl": "https://github.com/memedi42/MediArise-Releases/releases/download/v1.0.18/mediarise-release-1.0.18.apk",
  "apkSha256": "…",
  "apkSize": 3402726,
  "releaseNotes": "…",
  "publishedAt": "…"
}
```

`versionCode` es el único criterio para decidir si hay actualización: es el
mismo número que Android compara al instalar.
