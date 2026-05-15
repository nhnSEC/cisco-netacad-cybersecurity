# Lab 04 — Configuração do DHCP em um Roteador Wireless

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Configuração do DHCP em um Roteador Wireless (sem fio).pka`](./Configura%C3%A7%C3%A3o%20do%20DHCP%20em%20um%20Roteador%20Wireless%20%28sem%20fio%29.pka)

---

## 🎯 Objetivo

Configurar o serviço **DHCP** no roteador wireless para que os clientes recebam automaticamente endereço IP, máscara de sub-rede, gateway padrão e servidor DNS — sem necessidade de configuração manual.

---

## 📡 Topologia

```
[PC1] )))           [Roteador Wireless]
[PC2] ))) ── Wi-Fi ── (DHCP Server)  ──── [Internet]
[PC3] )))
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **DHCP** | Protocolo que distribui configurações IP automaticamente |
| **DORA** | Processo DHCP: Discover → Offer → Request → Acknowledge |
| **Pool de endereços** | Faixa de IPs disponíveis para distribuição |
| **Lease time** | Tempo de concessão do IP (após expirar, é renovado) |
| **Exclusão de IPs** | IPs reservados fora do pool (ex: do próprio roteador) |

---

## 🪜 Procedimento realizado

1. Acessei a interface do roteador (`192.168.1.1`)
2. Fui até **Configurações de LAN → DHCP Server**
3. Configurei o pool DHCP:

```
DHCP Server: Habilitado
Endereço inicial: 192.168.1.100
Endereço final:   192.168.1.200
Máscara:          255.255.255.0
Gateway padrão:   192.168.1.1
Servidor DNS:     8.8.8.8
Lease time:       24 horas
```

4. Salvei e reiniciei o serviço DHCP
5. Nos PCs clientes, configurei a interface de rede para **"Obter IP automaticamente"**
6. Executei `ipconfig /renew` (Windows) em cada cliente
7. Verifiquei os IPs recebidos com `ipconfig`

---

## 🔎 O que observei — Processo DORA em detalhe

```
PC (cliente)                    Roteador (servidor DHCP)
    │                                    │
    │── DISCOVER (broadcast) ──────────► │  "Tem algum servidor DHCP?"
    │                                    │
    │◄── OFFER ───────────────────────── │  "Sim! Aqui está o IP 192.168.1.100"
    │                                    │
    │── REQUEST (broadcast) ───────────► │  "Aceito o IP 192.168.1.100"
    │                                    │
    │◄── ACKNOWLEDGE ─────────────────── │  "Confirmado! IP é seu por 24h"
    │                                    │
```

---

## 📚 Diferença: IP Estático vs DHCP

| | IP Estático | DHCP Dinâmico |
|--|-------------|---------------|
| **Configuração** | Manual em cada dispositivo | Automática |
| **Uso ideal** | Servidores, impressoras, roteadores | PCs, celulares, laptops |
| **Risco** | Conflito de IPs se mal gerenciado | Dependência do servidor DHCP |
| **Gerenciamento** | Trabalhoso em redes grandes | Centralizado e eficiente |

---

## 💡 Aprendizados

- DHCP funciona via **broadcast** — por isso, o cliente não precisa saber nenhum IP antes de receber o seu.
- Em redes corporativas, o servidor DHCP geralmente é separado do roteador.
- O `ipconfig /release` libera o IP atual; `ipconfig /renew` solicita um novo.
- O IP do roteador (gateway) deve estar **fora** do pool DHCP para evitar conflitos.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
