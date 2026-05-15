# Lab 01 — A Interação do Cliente

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`A interação do cliente.pka`](./A%20intera%C3%A7%C3%A3o%20do%20cliente.pka)

---

## 🎯 Objetivo

Observar e entender como um cliente (navegador) interage com servidores de rede ao acessar uma página web, identificando o papel de protocolos como **DNS** e **HTTP** nesse processo.

---

## 📡 Topologia

```
[PC Cliente] ──── [Switch] ──── [Roteador] ──── [Servidor Web]
                                     │
                                [Servidor DNS]
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **DNS** | Traduz nomes de domínio (ex: `cisco.com`) em endereços IP |
| **HTTP** | Protocolo de transferência de páginas web (porta 80) |
| **Modelo cliente-servidor** | O cliente faz requisições; o servidor responde com recursos |
| **TCP 3-way handshake** | SYN → SYN-ACK → ACK antes de qualquer troca de dados |

---

## 🪜 Procedimento realizado

1. Aberto o Packet Tracer com a topologia pré-configurada
2. No PC Cliente, acessei o navegador e digitei o endereço do servidor web
3. Ativei o **modo simulação** para observar o fluxo de pacotes passo a passo
4. Observei a sequência:
   - PC envia consulta DNS ao servidor DNS
   - DNS responde com o IP do servidor web
   - PC inicia conexão TCP com o servidor web (handshake)
   - PC envia requisição HTTP GET
   - Servidor responde com a página HTML
5. Identifiquei as camadas OSI envolvidas em cada etapa

---

## 🔎 O que observei

- Antes de qualquer comunicação HTTP acontecer, o DNS é consultado — sem isso, o cliente não sabe para qual IP enviar a requisição.
- O TCP garante a entrega confiável: cada segmento é confirmado (ACK).
- No modo simulação, é possível ver o encapsulamento: HTTP dentro de TCP, dentro de IP, dentro de Ethernet.

---

## 📚 Camadas OSI envolvidas

| Camada | Protocolo ativo |
|--------|----------------|
| 7 — Aplicação | HTTP, DNS |
| 4 — Transporte | TCP (porta 80 para HTTP, porta 53 para DNS) |
| 3 — Rede | IP |
| 2 — Enlace | Ethernet |
| 1 — Física | Cabo UTP |

---

## 💡 Aprendizados

- O DNS é invisível para o usuário, mas é o primeiro passo de qualquer navegação web.
- O encapsulamento de dados funciona de cima pra baixo (do app até o fio) e o desencapsulamento de baixo pra cima no destino.
- O modelo de simulação do Packet Tracer é muito útil para visualizar o que normalmente não conseguimos ver.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.

