# Transcrip Audio

Transcripciones automáticas de vídeos de YouTube sobre la teoría de la Tierra Plana, generadas con [faster-whisper](https://github.com/SYSTRAN/faster-whisper).

## Archivos

| Audio | Transcripción |
|-------|--------------|
| `5 Argumentos Terraplanistas Desmontados [Q6PpUG9xxFU].opus` | `5 Argumentos Terraplanistas Desmontados [Q6PpUG9xxFU].txt` |
| `Conspiranoicos y científicos discuten sobre la TIERRA PLANA - Santaolalla "se quiere ir" [-G7Ud-PRoyY].opus` | `Conspiranoicos y científicos discuten sobre la TIERRA PLANA [...].txt` |
| `The Flat Earth Society: Interview With Mark Sargent [82HofUlhPNs].opus` | `The Flat Earth Society: Interview With Mark Sargent [82HofUlhPNs].txt` |

Los audios originales se encuentran en la carpeta `src/`.

## Descarga de audio con yt-dlp

Los archivos de audio fueron descargados directamente desde YouTube usando **[yt-dlp](https://github.com/yt-dlp/yt-dlp)**, un potente fork de youtube-dl con soporte para cientos de sitios y actualizaciones frecuentes.

### Instalación

```bash
# Con pip
pip install yt-dlp

# O con el binario precompilado (Linux)
sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```

### Comando utilizado

```bash
yt-dlp -x --audio-format opus --audio-quality 0 -o "%(title)s [%(id)s].%(ext)s" <URL>
```

- `-x` — extrae solo el audio (sin vídeo)
- `--audio-format opus` — convierte al formato Opus (buena calidad, tamaño reducido)
- `--audio-quality 0` — máxima calidad
- `-o "%(title)s [%(id)s].%(ext)s"` — nombre de archivo con título e ID del vídeo

### Referencias oficiales

- Repositorio: [https://github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp)
- Documentación de opciones: [https://github.com/yt-dlp/yt-dlp#usage-and-options](https://github.com/yt-dlp/yt-dlp#usage-and-options)
- Releases y binarios: [https://github.com/yt-dlp/yt-dlp/releases](https://github.com/yt-dlp/yt-dlp/releases)

## Transcripción

Las transcripciones se generaron con [faster-whisper](https://github.com/SYSTRAN/faster-whisper) usando el modelo `small`, ejecutado localmente en CPU. El proceso completo está documentado en el notebook [`transcripcion.ipynb`](transcripcion.ipynb).

```python
from faster_whisper import WhisperModel

model = WhisperModel("small", device="cpu", compute_type="int8")
segments, info = model.transcribe("audio.opus", language="es", beam_size=5)
```
