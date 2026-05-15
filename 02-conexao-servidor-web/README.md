# Lab 02 — Conexão com um Servidor da Web

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Conexão com um servidor da Web.pka`](./Conex%C3%A3o%20com%20um%20servidor%20da%20Web.pka)

---

## 🎯 Objetivo

Analisar detalhadamente o processo de conexão TCP entre um cliente e um servidor web, observando o handshake de três vias e o fluxo completo de uma requisição HTTP.

---

## 📡 Topologia

```
[PC Cliente] ──── [Switch] ──── [Servidor Web (HTTP)]
    │
 Navegador Web
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **TCP Handshake** | Processo de 3 etapas para estabelecer conexão confiável |
| **HTTP GET** | Requisição do cliente para buscar um recurso no servidor |
| **HTTP 200 OK** | Resposta de sucesso do servidor |
| **Porta 80** | Porta padrão do HTTP |
| **Número de sequência TCP** | Garante a ordem e integridade dos segmentos |

---

## 🪜 Procedimento realizado

1. Configurada a topologia com PC cliente e servidor web
2. Ativado o modo simulação com filtros para **TCP** e **HTTP**
3. Acessado o servidor web pelo navegador do PC
4. Observadas as seguintes etapas no modo simulação:

### Etapa 1 — TCP 3-way Handshake
```
Cliente → Servidor : SYN (quero me conectar)
Servidor → Cliente : SYN-ACK (aceito, confirmado)
Cliente → Servidor : ACK (conexão estabelecida)
```

### Etapa 2 — Requisição HTTP
```
Cliente → Servidor : HTTP GET /index.html
Servidor → Cliente : HTTP 200 OK + conteúdo HTML
```

### Etapa 3 — Encerramento TCP
```
Cliente → Servidor : FIN
Servidor → Cliente : ACK + FIN
Cliente → Servidor : ACK
```

5. Inspecionei os PDUs (Protocol Data Units) em cada camada

---

## 🔎 O que observei

- O TCP **não é opcional** — o HTTP depende dele para funcionar de forma confiável.
- Cada pacote tem cabeçalhos adicionados em cada camada (encapsulamento).
- O servidor precisa estar "ouvindo" na porta 80 para aceitar conexões HTTP.

---

## 📚 Camadas OSI envolvidas

| Camada | Protocolo ativo | PDU |
|--------|----------------|-----|
| 7 — Aplicação | HTTP | Mensagem |
| 4 — Transporte | TCP | Segmento |
| 3 — Rede | IP | Pacote |
| 2 — Enlace | Ethernet | Quadro |
| 1 — Física | UTP | Bits |

---

## 💡 Aprendizados

- O **handshake TCP** acontece antes de qualquer dado de aplicação ser enviado — é a "negociação" entre os dois lados.
- HTTP é **stateless**: cada requisição é independente, a conexão TCP pode ser encerrada após cada uma.
- O Packet Tracer permite ver o conteúdo de cada PDU clicando nos envelopes coloridos — excelente para visualizar encapsulamento.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
