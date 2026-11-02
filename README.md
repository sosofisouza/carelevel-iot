<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rounded&color=0:fbcfe8,100:f9a8d4&height=170&section=header&text=CareLevel%20IoT&fontSize=42&fontColor=831843&fontAlignY=42&desc=Monitoramento%20de%20sinais%20vitais%20em%20tempo%20real&descSize=16&descAlignY=68" width="100%" />

<img src="https://readme-typing-svg.demolab.com?font=Quicksand&weight=600&size=19&pause=1400&color=DB2777&center=true&vCenter=true&width=620&lines=ESP32+%2B+MQTT+com+TLS;Node-RED+%2B+InfluxDB;Do+simulador+ao+dispositivo+f%C3%ADsico" />

<br>

<a href="https://wokwi.com/projects/462732527805844481">Simular no Wokwi</a>
&nbsp;&nbsp;·&nbsp;&nbsp;
<a href="https://youtu.be/tui7DMzma-o">Assistir ao vídeo</a>

</div>

<br>

### Sobre o projeto

Parte IoT do **CareLevel**, solução desenvolvida no Challenge CarePlus da FIAP. Um ESP32, simulado no Wokwi, lê **frequência cardíaca, saturação de oxigênio e temperatura corporal**, envia os dados por **MQTT com TLS** para o HiveMQ Cloud e o **Node-RED** processa e exibe as informações.

O projeto evoluiu em duas sprints:

| Sprint | O que foi feito |
|:---|:---|
| **Sprint 2** | Simulação no Wokwi com ESP32 e DHT22, BPM e SpO2 simulados, e dashboard em tempo real no Node-RED |
| **Sprint 3** | Nova versão do firmware com os sensores MAX30100 e DHT11, e gravação do histórico no InfluxDB Cloud |

<br>

### Arquitetura

```
ESP32 (Wokwi) ── MQTT/TLS ──►  HiveMQ Cloud  ──►  Node-RED  ──►  Dashboard
                                    (broker)          (fluxos)  ──►  InfluxDB Cloud
```

Detalhes no [documento de arquitetura](./docs/CareLevel_IoT_Architecture.pdf), no [fluxograma do firmware](./docs/fluxograma.jpeg) e no [diagrama da Sprint 3](./docs/arquitetura-sprint3.png).

<br>

### Componentes (Sprint 3)

| Componente | Função | Ligação no ESP32 |
|:---|:---|:---|
| ESP32 DevKit | Microcontrolador com Wi-Fi | — |
| MAX30100 | Batimentos (BPM) e oxigênio (SpO2) | I2C: SDA no GPIO 21, SCL no GPIO 22 |
| DHT11 | Temperatura | GPIO 5 |

<br>

### Tópicos MQTT

| Tópico | Exemplo de mensagem |
|:---|:---|
| `carelevel/saude/bpm` | `{"bpm": 72.0}` |
| `carelevel/saude/spo2` | `{"spo2": 98.0}` |
| `carelevel/saude/temperatura` | `{"temperatura": 36.70}` |
| `carelevel/saude/temp_valida` | `{"temp_valida": true}` |

Os dados são publicados a cada 5 segundos. Se o sensor de temperatura falhar, o firmware envia `temp_valida = false` e usa 36,5 °C como valor de reserva.

<br>

### Tecnologias

<div align="center">
  <img src="https://skillicons.dev/icons?i=arduino,cpp&theme=light" />
  <br>
  <sub>ESP32 · C++ · MQTT · HiveMQ Cloud · Node-RED · InfluxDB · Wokwi</sub>
</div>

<br>

### Como executar

**1. Broker:** crie um cluster gratuito no HiveMQ Cloud e um usuário com senha.

**2. Firmware:** abra `firmware/CareLevel_FisicoFinal/CareLevel_FisicoFinal.ino` na Arduino IDE, instale as bibliotecas (Adafruit Unified Sensor, ArduinoJson, DHT sensor library, MAX30100lib e PubSubClient) e troque os valores `SUA_REDE_WIFI`, `SUA_SENHA_WIFI`, `SEU_USUARIO_MQTT` e `SUA_SENHA_MQTT` pelos seus.

**3. Node-RED:** instale o `node-red-contrib-influxdb`, importe `platform/node-red/flows.json` e preencha as credenciais do broker e do InfluxDB nos nós de configuração.

**Simulação:** abra o [projeto no Wokwi](https://wokwi.com/projects/462732527805844481).

<br>

### Estrutura

```
carelevel-iot/
├── firmware/CareLevel_FisicoFinal/   código do ESP32
├── platform/node-red/flows.json      fluxo do Node-RED
└── docs/                             arquitetura e fluxograma
```

<br>

### Equipe

<div align="center">

Camile Silva &nbsp;·&nbsp; Gustavo Ferreira &nbsp;·&nbsp; Lucas Caetano &nbsp;·&nbsp; Marco Conte &nbsp;·&nbsp; Sofia Rodrigues

</div>

<img src="https://capsule-render.vercel.app/api?type=rounded&color=0:fbcfe8,100:f9a8d4&height=60&section=footer" width="100%" />
