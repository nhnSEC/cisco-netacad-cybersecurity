# Lab 06 — Examinando o NAT em um Roteador Sem Fio

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Examinando o NAT em um roteador sem fio.pka`](./Examinando%20o%20NAT%20em%20um%20roteador%20sem%20fio.pka)

---

## 🎯 Objetivo

Observar como o **NAT (Network Address Translation)** funciona em um roteador wireless, entendendo como múltiplos dispositivos com IPs privados compartilham um único IP público para acessar a internet.

---

## 📡 Topologia

```
[PC1] 192.168.0.10 ┐
[PC2] 192.168.0.11 ├── [Roteador Wireless] ──── [Internet]
[PC3] 192.168.0.12 ┘      NAT/PAT           IP Público: 203.0.113.5
         ↑
    IPs Privados
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **NAT** | Traduz IPs privados em IP público e vice-versa |
| **PAT** | NAT com tradução de portas — permite múltiplos clientes no mesmo IP |
| **IP Privado** | Faixas reservadas: 10.x.x.x, 172.16-31.x.x, 192.168.x.x |
| **IP Público** | Endereço roteável na internet, único globalmente |
| **Tabela NAT** | Registro das traduções ativas no roteador |

---

## 🪜 Procedimento realizado

1. Ativado o modo simulação para capturar tráfego
2. PC1 (`192.168.0.10`) acessou um servidor web externo
3. Observei os pacotes **antes e depois** do roteador:

**Pacote saindo do PC1 (antes do NAT):**
```
IP de origem:  192.168.0.10 (privado)
IP de destino: 203.0.113.100 (servidor web)
Porta origem:  49152
```

**Pacote após passar pelo roteador (depois do NAT):**
```
IP de origem:  203.0.113.5 (IP público do roteador)
IP de destino: 203.0.113.100 (servidor web)
Porta origem:  50001  ← PAT substitui a porta também
```

4. Visualizei a tabela NAT no roteador
5. Observei o caminho de volta: servidor responde ao IP público, roteador consulta tabela e encaminha para PC1

---

## 🔎 Como o NAT/PAT funciona

```
SAÍDA (PC → Internet):
  PC1: 192.168.0.10:49152  →  [Roteador NAT]  →  203.0.113.5:50001

RETORNO (Internet → PC):
  203.0.113.5:50001  →  [Roteador NAT]  →  192.168.0.10:49152
  (roteador consulta tabela e sabe que 50001 pertence ao PC1)
```

---

## 📚 Faixas de IP Privado (RFC 1918)

| Classe | Faixa | Sub-rede padrão |
|--------|-------|-----------------|
| A | 10.0.0.0 – 10.255.255.255 | /8 |
| B | 172.16.0.0 – 172.31.255.255 | /12 |
| C | 192.168.0.0 – 192.168.255.255 | /16 |

> IPs privados **não são roteados** na internet pública — por isso o NAT é necessário.

---

## 💡 Aprendizados

- O NAT foi criado para resolver o esgotamento de IPs IPv4 — com ele, toda uma rede doméstica usa apenas 1 IP público.
- O PAT (também chamado NAT overload) usa as **portas TCP/UDP** como diferenciador — por isso consegue atender centenas de clientes simultâneos.
- Com **IPv6**, o NAT teoricamente não seria necessário (há IPs suficientes para todos os dispositivos), mas o NAT ainda é comum por segurança.
- Uma consequência do NAT: dispositivos na rede interna **não são acessíveis diretamente** da internet — isso é um benefício de segurança acidental.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
