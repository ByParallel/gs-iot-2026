# 🚀 Plataforma de Lançamento Espacial — FIAP GS 2026.1

**Physical Computing, Embedded AI, Robotics & Cognitive IoT**

| Integrante | RM |
|---|---|
| Arthur Batista | RM 565346 |
| Joao Pedro | RM 561738 |
| Nelson Felix | RM 565603 |

---

## 📋 Descrição

Solução IoT completa para monitoramento em tempo real de uma plataforma de lançamento espacial. O sistema detecta condições críticas como vazamento de gás, temperatura elevada e invasão na zona de exclusão, classificando o risco em 4 estados e disparando alertas automáticos.

---

## 🏗️ Arquitetura

```
ESP32 (Wokwi) → MQTT (HiveMQ Cloud) → n8n → Supabase (PostgreSQL)
                                         ↓
                                    Telegram Bot (alertas)
                                         ↓
                              Dashboard HTML (tempo real)
                              Grafana Cloud (histórico)
```

---

## 🔧 Hardware — ESP32 (Wokwi)

| Sensor/Atuador | Pino | Função |
|---|---|---|
| DHT22 | 15 | Temperatura e Umidade |
| MQ-2 (AOUT) | 34 | Concentração de gás (%) |
| MQ-2 (DOUT) | 35 | Alarme digital de gás |
| HC-SR04 | 5/19 | Distância — detecção de intruso |
| LED Verde | 2 | Estado LIVRE |
| LED Amarelo | 4 | Estado ATENÇÃO |
| LED Vermelho | 13 | Estado PERIGO/CRÍTICO |
| LED Azul | 26 | Estado CRÍTICO / Controle remoto |
| Buzzer | 14 | Alarme sonoro |

---

## 🚦 Estados do Sistema

| Estado | Condição | Indicadores |
|---|---|---|
| **LIVRE** | Tudo normal | LED verde piscando |
| **ATENÇÃO** | Temp > 40°C ou objeto se aproximando | LED amarelo |
| **PERIGO** | Gás detectado OU intruso < 150cm | LED vermelho + buzzer |
| **CRÍTICO** | Gás + Temperatura crítica | Todos LEDs + buzzer alternado |

---

## 📡 Tópicos MQTT

| Tópico | Uso |
|---|---|
| `fiap/iot/lancamento/PLT-01/telemetria` | Dados normais (LIVRE/ATENÇÃO) |
| `fiap/iot/lancamento/PLT-01/alerta` | Alertas (PERIGO/CRÍTICO) |
| `fiap/iot/lancamento/PLT-01/comando` | Controle remoto do ESP32 |

---

## 🎮 Inovação — Controle Remoto Bidirecional

O dashboard permite enviar comandos ao ESP32 via MQTT:

| Comando | Ação |
|---|---|
| `LED_AZUL_ON` | Acende LED azul remotamente |
| `LED_AZUL_OFF` | Apaga LED azul remotamente |
| `BUZZER_ON` | Aciona buzzer por 500ms |
| `RESET` | Reseta todos os estados remotos |

---

## 📁 Arquivos

| Arquivo | Descrição |
|---|---|
| `main.cpp` | Código do ESP32 |
| `diagram.json` | Circuito Wokwi |
| `dashboard_gs.html` | Dashboard tempo real |
| `n8n_workflow_gs.json` | Workflow n8n |
| `grafana_dashboard.json` | Dashboard Grafana |
| `Relatorio_GS_2026_1_IoT.pdf` | Relatório completo |
| `VIDEO.mp4` | Pitch de apresentação |

---

## 🛠️ Como executar

1. Abra o projeto no [Wokwi](https://wokwi.com) com o `diagram.json` e `main.cpp`
2. Importe o `n8n_workflow_gs.json` no n8n e configure as credenciais MQTT
3. Abra o `dashboard_gs.html` no browser
4. Importe o `grafana_dashboard.json` no Grafana Cloud conectado ao Supabase

---

**FIAP — Tecnologia em Inteligência Artificial — 2TIAP — 2026**
