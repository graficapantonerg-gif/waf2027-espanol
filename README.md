# WE ARE FOOTBALL 2027 — Traducción al español

**Parche que traduce los 2.434 textos que el juego dejó sin traducir.**

[![Descargar](https://img.shields.io/badge/Descargar-v1.0-brightgreen?style=for-the-badge)](https://github.com/graficapantonerg-gif/waf2027-espanol/releases/latest)
[![Ko-fi](https://img.shields.io/badge/Invitame_un_café-Ko--fi-ff5e5b?style=for-the-badge)](https://ko-fi.com/pantone)

---

## El problema

WE ARE FOOTBALL 2027 **ya trae español de fábrica**, pero el archivo de idioma del estudio está a medio terminar:

| | |
|---|---|
| Textos que faltan por completo | **445** |
| Textos que existen pero están **vacíos** | **1.996** |
| **Total sin traducir** | **2.434** |

El juego **no hace fallback a inglés**: dibuja esos textos en blanco. Por eso aparecen botones vacíos, tooltips sin texto y pantallas a medias.

El caso más visible es la **selección de base de datos** al empezar una partida: los dos botones salen completamente en blanco.

<table>
<tr><th>Sin el parche</th><th>Con el parche</th></tr>
<tr><td><code>[          ]</code><br><code>[          ]</code></td><td><code>[ Estándar ]</code><br><code>[  Mundo   ]</code></td></tr>
</table>

## La solución

Este parche traduce los 2.434 textos y deja el juego **sin un solo hueco**.

### Qué se tradujo

- Botones, etiquetas, columnas de tablas y menús
- Todos los tooltips del **Game Tuning**
- **Glosario** completo y textos de ayuda de pantalla
- Narración del partido: goles, tarjetas, lesiones, VAR, penales
- Negociaciones, contratos y cláusulas
- Titulares de diario
- **Logros de Steam**
- Comentarios de los hinchas
- Eventos de entrenamiento, fiestas y crisis
- Modo Creativo y modo Espectador
- Descripciones de **150 ciudades y 51 países**
- Tutoriales

### Errores del original que se corrigieron de paso

- Una entrada que estaba **en alemán** dentro del archivo inglés (`ID_VERHANDLUNG_AUSWIRKUNG_VERSPRECHEN_3`)
- Fechas capicúa con el mes y el día invertidos — el chiste no funcionaba (`02/25/2052` → `25/02/2052`)
- Varios marcadores `{FF#...}` mal formados que se imprimían literales en pantalla
- Una clave duplicada con un tabulador en vez de un espacio

## Instalación

1. Descargá el ZIP desde [**Releases**](https://github.com/graficapantonerg-gif/waf2027-espanol/releases/latest)
2. Descomprimilo donde quieras
3. Botón derecho en `aplicar-parche.ps1` → **Ejecutar con PowerShell**
4. Abrí el juego

El script busca solo tu carpeta del juego (incluida la de Steam). Si no la encuentra, te la pide: es la que tiene `waf2027.exe` adentro.

> Si Windows bloquea los scripts, abrí PowerShell en esa carpeta y corré:
> ```powershell
> powershell -ExecutionPolicy Bypass -File .\aplicar-parche.ps1
> ```

## Cómo funciona (y por qué pesa 151 KB)

El ZIP **no trae el archivo de idioma del juego**. Trae solo las 2.434 líneas traducidas, y el script arma el archivo final **en tu máquina** usando el `GameText_es-es.txt` y el `GameText_en-uk.txt` que ya vienen en tu propia copia, en `Editor\Translation`.

Así no se redistribuye nada del estudio, y el paquete pesa 151 KB en vez de 2,6 MB.

El resultado se escribe en:

```
<juego>\datafiles\gamedata\waf27\GameText_es-es.txt
%USERPROFILE%\Saved Games\We Are Football\datafiles\gamedata\waf27\GameText_es-es.txt
```

**No toca `datafiles.wsz` ni ningún archivo original del juego.** También deja `"languageId":5` en `settings.conf`, con backup del original.

## Volver al inglés

Borrá los dos `GameText_es-es.txt` de arriba, o poné `"languageId":1` en:

```
%USERPROFILE%\Saved Games\We Are Football\waf2027\settings.conf
```

## Compatibilidad

Probado en la build **2026_09_15 (Build160_CL33704)**.

Debería andar en cualquier versión que traiga la carpeta `Editor\Translation`. Si una actualización agrega textos nuevos, esos van a salir en inglés hasta que actualice el parche — nada se rompe.

Si una actualización pisa el archivo, volvé a correr `aplicar-parche.ps1`. No pasa nada por correrlo varias veces.

## Control de calidad

Chequeos automáticos sobre el archivo final:

- 28.910 claves, **mismo orden** que el archivo inglés
- **0** entradas vacías que no deberían estarlo
- **0** entradas que quedaron en inglés
- Todos los marcadores del motor (`{playerid1:PLAYER}`, `{FF#masc|fem}`, `{amount1:MONEY}`…) verificados uno por uno contra el original
- El script se probó en limpio: borrando el archivo instalado y regenerándolo desde cero, el resultado da el **mismo MD5**

---

**Libre de compartir.** Por favor no lo metas detrás de un acortador con publicidad.

Si te sirvió, [invitame un café](https://ko-fi.com/pantone) ☕
