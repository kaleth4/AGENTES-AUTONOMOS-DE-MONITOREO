# 🤖 Agentes Autónomos y Sistemas "Agentivos"

Sistema de monitoreo autónomo de sitios web que se "despierta" periódicamente para verificar la salud de sitios, autocorregir problemas y enviar reportes.

## ✨ Características

- **Monitoreo continuo**: Verifica la disponibilidad y rendimiento de sitios web
- **Autocorrección**: Intenta solucionar problemas automáticamente
- **Reportes via Discord**: Envía notificaciones de estado
- **Orquestación multi-agente**: Gestiona múltiples agentes distribuidos

## 🚀 Instalación

```bash
# Clonar o navegar al proyecto
cd agentes-autonomos-monitoreo

# Crear entorno virtual
python -m venv venv

# Activar entorno
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate    # Windows

# Instalar dependencias
pip install -r requirements.txt
```

## 📋 Requisitos

```
playwright
asyncio
discord.py
```

## ⚙️ Configuración

Edita `main.py` y configura:

```python
URLS_MONITOREO = [
    "https://tusitio1.com",
    "https://tusitio2.com"
]
DISCORD_WEBHOOK_URL = "tu-webhook-url"
INTERVALO_MINUTOS = 5  # Intervalo entre verificaciones
```

## 🏃 Uso

### Ejecutar agente individual
```bash
python main.py
```

### Ejecutar con orquestador de múltiples agentes
```python
from main import AgenteMonitoreo, OrquestadorAgentes
import asyncio

async def main():
    orquestador = OrquestadorAgentes()
    
    # Crear agentes para diferentes regiones
    agente_us = AgenteMonitoreo()
    agente_eu = AgenteMonitoreo()
    
    orquestador.registrar_agente("us-east", agente_us)
    orquestador.registrar_agente("eu-west", agente_eu)
    
    await orquestador.ejecutar_todos()

asyncio.run(main())
```

## 📊 Reportes

El sistema genera reportes automáticos con:
- Estado de cada sitio (✅ operativo / ❌ error)
- Tiempo de carga
- Errores detectados
- Intentos de autocorrección

## 🔄 Arquitectura

```
┌─────────────────────────────────────────┐
│         Orquestador de Agentes           │
├─────────────────────────────────────────┤
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ │
│  │ Agente 1 │ │ Agente 2 │ │ Agente 3 │ │
│  │ (US)     │ │ (EU)     │ │ (ASIA)   │ │
│  └────┬─────┘ └────┬─────┘ └────┬─────┘ │
│       └────────────┼────────────┘       │
│                    ▼                    │
│         ┌──────────────────┐           │
│         │  Verificación    │           │
│         │  con Playwright  │           │
│         └────────┬─────────┘           │
│                  │                      │
│         ┌────────▼─────────┐            │
│         │  Autocorrección │            │
│         └────────┬─────────┘            │
│                  │                      │
│         ┌────────▼─────────┐            │
│         │  Reporte Discord │            │
│         └──────────────────┘            │
└─────────────────────────────────────────┘
```

## 🛠️ Extensión

Puedes extender el agente implementando:
- Nuevos métodos de autocorrección
- Integraciones con más notificaciones (Slack, Email, SMS)
- Análisis de métricas más profundo
- Integración con herramientas de infraestructura (AWS, GCP, Azure)

## 📄 Licencia

MIT License - Libre para uso personal y comercial.
