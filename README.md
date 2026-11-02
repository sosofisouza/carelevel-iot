<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rounded&color=0:fbcfe8,100:f9a8d4&height=170&section=header&text=CareLevel%20IoT&fontSize=42&fontColor=831843&fontAlignY=42&desc=Monitoramento%20de%20sinais%20vitais%20em%20tempo%20real&descSize=16&descAlignY=68" width="100%" />

<img src="https://readme-typing-svg.demolab.com?font=Quicksand&weight=600&size=19&pause=1400&color=DB2777&center=true&vCenter=true&width=620&lines=ESP32+%2B+MQTT+com+TLS+%2B+Node-RED;Batimentos%2C+oxig%C3%AAnio+e+temperatura;Dashboard+em+tempo+real" />

<br>

<a href="https://wokwi.com/projects/462732527805844481">Simular no Wokwi</a>
&nbsp;&nbsp;·&nbsp;&nbsp;
<a href="https://youtu.be/tui7DMzma-o">Assistir ao vídeo</a>

</div>

<br>

### Sobre o projeto

Sistema IoT da plataforma **CareLevel**, desenvolvido na disciplina de Edge Computing da FIAP. Um ESP32 lê os sinais vitais, envia os dados por **MQTT com TLS** para a nuvem, e o **Node-RED** exibe tudo em um dashboard em tempo real.

<br>

### Arquitetura

```
ESP32 + DHT22  ── MQTT/TLS ──►  HiveMQ Cloud  ──►  Node-RED  ──►  Dashboard
   (Wokwi)                        (broker)         (fluxos)      (tempo real)
```

Detalhes no [documento de arquitetura](./CareLevel_IoT_Architecture.pdf) e no [fluxograma do firmware](./fluxograma.jpeg).

<br>

### Funcionalidades

- Conexão Wi-Fi com reconexão automática
- MQTT seguro via TLS na porta 8883
- Temperatura pelo DHT22, com valor de reserva se o sensor falhar
- BPM (60 a 100) e SpO2 (95% a 100%) simulados
- Envio dos dados em JSON a cada 5 segundos
- Dashboard em tempo real no Node-RED

<br>

### Tópicos MQTT

| Tópico | Exemplo de mensagem |
|:---|:---|
| `carelevel/saude/bpm` | `{"bpm": 72.0}` |
| `carelevel/saude/spo2` | `{"spo2": 98.0}` |
| `carelevel/saude/temperatura` | `{"temperatura": 36.70}` |
| `carelevel/saude/temp_valida` | `{"temp_valida": true}` |

<br>

### Tecnologias

<div align="center">
  <img src="https://skillicons.dev/icons?i=arduino,cpp&theme=light" />
  <br>
  <sub>ESP32 · C++ · MQTT · HiveMQ Cloud · Node-RED · Wokwi</sub>
</div>

<br>

### Como executar

**1. Simulação:** abra o [projeto no Wokwi](https://wokwi.com/projects/462732527805844481), clique em *Play* e acompanhe o Monitor Serial.

**2. Node-RED:**

```bash
npm install -g node-red
node-red
```

No editor (`http://localhost:1880`), instale o `node-red-dashboard`, crie os nós MQTT assinando os tópicos acima e preencha as credenciais do seu broker. O dashboard fica em `http://localhost:1880/ui`.

O código do firmware está no [projeto do Wokwi](https://wokwi.com/projects/462732527805844481).

<br>

### Equipe

<div align="center">

Camile Silva &nbsp;·&nbsp; Gustavo Ferreira &nbsp;·&nbsp; Lucas Caetano &nbsp;·&nbsp; Marco Conte &nbsp;·&nbsp; Sofia Rodrigues

</div>

<img src="https://capsule-render.vercel.app/api?type=rounded&color=0:fbcfe8,100:f9a8d4&height=60&section=footer" width="100%" />
