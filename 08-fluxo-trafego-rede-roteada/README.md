# Lab 08 — Observar o Fluxo de Tráfego em uma Rede Roteada

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Observar o fluxo de tráfego em uma rede roteada.pka`](./Observar%20o%20fluxo%20de%20tr%C3%A1fego%20em%20uma%20rede%20roteada.pka)

---

## 🎯 Objetivo

Observar como os pacotes percorrem múltiplas redes passando por um roteador, entendendo o papel do roteamento IP e como o endereço MAC e IP mudam (ou não) ao longo do caminho.

---

## 📡 Topologia

```
[PC1] 192.168.1.10          [PC2] 192.168.2.10
  └── [Switch A]──[Roteador]──[Switch B]──┘
      Rede 1                     Rede 2
   192.168.1.0/24           192.168.2.0/24
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **Roteamento** | Processo de encaminhar pacotes entre redes diferentes |
| **Gateway padrão** | IP do roteador configurado nos PCs para sair da rede local |
| **TTL** | Time to Live — decrementa a cada salto; evita loops |
| **ICMP** | Protocolo de controle de mensagens (usado pelo ping) |
| **Salto (hop)** | Cada passagem por um roteador conta como um salto |

---

## 🪜 Procedimento realizado

1. Configurei os PCs com gateway apontando para o roteador
2. Ativei modo simulação com filtros para **ICMP** e **ARP**
3. PC1 (`192.168.1.10`) fez ping para PC2 (`192.168.2.10`)
4. Observei cada salto:

**PC1 → Roteador:**
```
MAC origem:  MAC do PC1
MAC destino: MAC da interface do roteador (Gi0/0)
IP origem:   192.168.1.10  ← não muda
IP destino:  192.168.2.10  ← não muda
```

**Roteador → PC2:**
```
MAC origem:  MAC da interface do roteador (Gi0/1)  ← MUDOU!
MAC destino: MAC do PC2                             ← MUDOU!
IP origem:   192.168.1.10  ← não mudou
IP destino:  192.168.2.10  ← não mudou
```

5. Executei `tracert 192.168.2.10` para ver os saltos

---

## 💡 Aprendizados

- O **endereço IP não muda** ao longo do caminho — é o identificador do destino final.
- O **endereço MAC muda** a cada salto — é só para entrega local entre dispositivos adjacentes.
- O roteador **descarta o quadro Ethernet** recebido e cria um novo para a próxima rede.
- O `traceroute` / `tracert` usa TTL decrescente para mapear cada salto no caminho.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
