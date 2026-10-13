<p align="center">
  <a href="https://github.com/Dathinel/rodaje"><img src="https://raw.githubusercontent.com/Dathinel/rodaje/main/assets/marca/rodaje.svg" alt="Logotipo de Rodaje" width="104"></a>
</p>

<h1 align="center">modulo-vision</h1>

<p align="center">
  Módulo de IA opcional para <a href="https://github.com/Dathinel/rodaje">Rodaje</a>: quita el fondo de las personas, detecta rostros y personas y calcula un reencuadre que sigue al sujeto. Todo corre en tu equipo, sin conexión.
</p>

<p align="center">
  <a href="#licencia"><img src="https://img.shields.io/badge/c%C3%B3digo-GPLv3-E8833A?style=flat-square&labelColor=1D1D1D" alt="Código GPLv3"></a>
  <a href="https://github.com/Dathinel/modulo-vision/releases/latest"><img src="https://img.shields.io/github/v/release/Dathinel/modulo-vision?style=flat-square&labelColor=1D1D1D&color=E8833A&label=versi%C3%B3n" alt="Última versión"></a>
  <img src="https://img.shields.io/badge/contenido-3_funciones_%C2%B7_4_modelos-E8833A?style=flat-square&labelColor=1D1D1D" alt="Contenido: 3 funciones · 4 modelos">
  <img src="https://img.shields.io/badge/formato-.paquete-E8833A?style=flat-square&labelColor=1D1D1D" alt="Formato .paquete">
  <a href="https://github.com/Dathinel/rodaje"><img src="https://img.shields.io/badge/para-Rodaje-E8833A?style=flat-square&labelColor=1D1D1D" alt="Para Rodaje"></a>
</p>

| Función | Qué hace |
|---|---|
| `quitar-fondo` | Quitar el fondo (MODNet; «alta»: BiRefNet_lite) |
| `detectar` | Detectar rostros (YuNet) o personas (RT-DETRv2) |
| `reencuadre` | Reencuadre automático que sigue al sujeto |

Corre en: DirectML (GPU) o CPU. Motor: ONNX Runtime con DirectML 1.24.4 (MIT) y DirectML 1.15.4 (licencia de Microsoft). Rodaje lo abre como un proceso aparte y le habla por una tubería con nombre ([protocolo de módulos](https://github.com/Dathinel/rodaje/blob/main/docs/protocolo-modulos.md)); lo que devuelve es una propuesta que se aplica como un paso del historial (Ctrl+Z la deshace).

Desde 1.1, Rodaje le pasa con su perfil de IA el lado de trabajo de MODNet (`lado`), los hilos de la CPU (`hilos`) y cuántos cuadros infiere a la vez en la CPU (`paralelo`), y manda la calidad alta a la CPU si BiRefNet_lite no cabe en la GPU.

## Modelos (211 MB)

El `.paquete` no trae los modelos: Rodaje los baja después de instalar el módulo, comprueba su SHA-256 y los deja en `modelos\` dentro de la carpeta del módulo. Si la descarga se corta, sigue desde donde quedó.

| Id | Tamaño | Licencia | De dónde sale |
|---|---|---|---|
| `modnet` | 25 MB | Apache-2.0 | Hugging Face `Xenova/modnet` @ `fa2fa546` |
| `birefnet-lite-fp16` | 109 MB | MIT | Hugging Face `onnx-community/BiRefNet_lite-ONNX` @ `de15b22b` |
| `yunet-2023mar` | 227 KB | MIT | Hugging Face `opencv/face_detection_yunet` @ `3cc26e7f` |
| `rtdetr-v2-r18` | 77 MB | Apache-2.0 | Hugging Face `onnx-community/rtdetr_v2_r18vd-ONNX` @ `936f90b6` |

## Instalar en Rodaje

En Rodaje, Complementos → Instalar lo baja, comprueba la firma del catálogo y el hash, lo instala y baja sus modelos. A mano: descarga `modulo-vision-<versión>.paquete` de las [releases](https://github.com/Dathinel/modulo-vision/releases) y usa «Instalar desde archivo…» en Complementos; después, «Bajar modelos». Más detalles en la [guía de complementos](https://github.com/Dathinel/rodaje/blob/main/docs/guia/complementos.md).

## Código

El código fuente está en el repositorio de Rodaje, en [`modules/Rodaje.Module.Vision`](https://github.com/Dathinel/rodaje/tree/main/modules/Rodaje.Module.Vision), junto con la biblioteca del protocolo ([`src/Rodaje.Modules.Protocol`](https://github.com/Dathinel/rodaje/tree/main/src/Rodaje.Modules.Protocol)). Cada release adjunta además el código exacto con el que se compiló (`codigo-fuente-*.zip`). Se arma con:

```
powershell -NoProfile -ExecutionPolicy Bypass -File build\empaquetar-modulo.ps1 -Modulo modulo-vision
```

| Archivo | Qué es |
|---|---|
| `paquete.json` | El manifiesto del módulo: funciones, VRAM y cada modelo con su URL, tamaño y SHA-256 |
| `LICENCIAS.md` | Licencias de las bibliotecas y los modelos |
| `LICENSE` | GPLv3 con los términos adicionales de Rodaje |

## Licencia

El código es GPL-3.0-only con los términos adicionales de Rodaje (atribución y permiso para complementos), ver `LICENSE`. Los modelos y las bibliotecas conservan la suya: ver `LICENCIAS.md`. El logotipo de Rodaje es marca de su autor ([TRADEMARK.md](https://github.com/Dathinel/rodaje/blob/main/TRADEMARK.md)).
