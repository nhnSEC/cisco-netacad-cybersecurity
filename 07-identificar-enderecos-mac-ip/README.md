# Lab 07 — Identificar Endereços MAC e IP

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Identificar endereços MAC e IP.pka`](./Identificar%20endere%C3%A7os%20MAC%20e%20IP.pka)

---

## 🎯 Objetivo

Identificar e diferenciar endereços **MAC** (camada 2) e **IP** (camada 3) em dispositivos de rede, observando como o protocolo **ARP** faz a ponte entre esses dois tipos de endereçamento.

---

## 📡 Topologia

```
[PC1] ──┐
[PC2] ──┤── [Switch] ──── [Roteador] ──── [Servidor]
[PC3] ──┘
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **Endereço MAC** | 48 bits, gravado no hardware da NIC, único globalmente |
| **Endereço IP** | 32 bits (IPv4), lógico, configurável, identifica localização na rede |
| **ARP** | Protocolo que descobre o MAC a partir do IP conhecido |
| **Tabela ARP** | Cache local mapeando IP ↔ MAC |
| **Broadcast** | Envio para todos os dispositivos da rede (FF:FF:FF:FF:FF:FF) |

---

## 🪜 Procedimento realizado

1. Verifiquei o endereço MAC e IP de cada PC com `ipconfig /all`

**Exemplo — PC1:**
```
Endereço MAC:  00:1A:2B:3C:4D:5E
Endereço IP:   192.168.1.10
Máscara:       255.255.255.0
Gateway:       192.168.1.1
```

2. Ativei o modo simulação com filtro **ARP**
3. PC1 fez ping para PC2 (`192.168.1.11`) — PC1 não conhecia o MAC de PC2
4. Observei o processo ARP:

```
PC1 → Broadcast: "Quem tem o IP 192.168.1.11? Me diga seu MAC"
PC2 → PC1: "Sou eu! Meu MAC é 00:2B:3C:4D:5E:6F"
```

5. Verifiquei a tabela ARP com `arp -a`
6. Identifiquei endereços MAC e IP no modo de inspeção de PDU

---

## 🔎 Diferença fundamental: MAC vs IP

| | Endereço MAC | Endereço IP |
|--|-------------|-------------|
| **Camada** | 2 — Enlace de dados | 3 — Rede |
| **Formato** | `00:1A:2B:3C:4D:5E` | `192.168.1.10` |
| **Tamanho** | 48 bits (6 bytes) | 32 bits (IPv4) |
| **Atribuição** | Gravado no hardware (NIC) | Configurado (estático ou DHCP) |
| **Escopo** | Local (dentro da rede) | Global (entre redes) |
| **Muda?** | Não (pode ser falsificado por software) | Sim (quando muda de rede) |

---

## 🔎 O papel do ARP

- O switch usa o **MAC** para entregar quadros dentro da LAN.
- O roteador usa o **IP** para encaminhar pacotes entre redes.
- O ARP é o "tradutor" entre os dois mundos — sem ele, a comunicação L3 dentro de uma LAN seria impossível.

---

## 💡 Aprendizados

- Um pacote IP **sempre** precisa de um quadro Ethernet para ser transportado — e o quadro precisa do MAC de destino.
- O **ARP Spoofing** é um ataque que explora o ARP, enviando respostas falsas para redirecionar tráfego (Man-in-the-Middle).
- A tabela ARP tem um tempo de expiração — IPs que ficam muito tempo sem comunicação são removidos da cache.
- No roteador, cada interface tem seu próprio MAC e IP.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
