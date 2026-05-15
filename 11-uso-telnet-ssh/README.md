# Lab 11 — Uso do Telnet e SSH

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Uso do Telnet e SSH.pka`](./Uso%20do%20Telnet%20e%20SSH.pka)

---

## 🎯 Objetivo

Comparar o acesso remoto via **Telnet** (inseguro) e **SSH** (seguro) a dispositivos de rede, entendendo as diferenças de segurança e configurando o SSH em um roteador Cisco.

---

## 📡 Topologia

```
[PC Admin] ──── [Switch] ──── [Roteador Cisco]
                              Telnet: porta 23
                              SSH:    porta 22
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **Telnet** | Acesso remoto em texto plano — sem criptografia (porta 23) |
| **SSH** | Acesso remoto criptografado com autenticação forte (porta 22) |
| **VTY Lines** | Linhas virtuais de terminal no roteador (0–15) |
| **RSA Key** | Par de chaves usado pelo SSH para criptografia |
| **enable secret** | Senha criptografada para modo privilegiado |

---

## 🪜 Procedimento realizado

### Parte 1 — Testando Telnet (inseguro)

```cmd
telnet 192.168.1.1
```

No modo simulação, observei que **usuário e senha trafegam em texto plano** — qualquer sniffing de rede expõe as credenciais.

---

### Parte 2 — Configurando SSH no Roteador

```
Router> enable
Router# configure terminal

! Definir hostname (obrigatório para SSH)
Router(config)# hostname R1

! Definir domínio (obrigatório para gerar chave RSA)
R1(config)# ip domain-name netacad.lab

! Criar usuário local
R1(config)# username admin privilege 15 secret Senha@123

! Gerar par de chaves RSA (2048 bits = recomendado)
R1(config)# crypto key generate rsa modulus 2048

! Configurar SSH versão 2 (mais seguro que v1)
R1(config)# ip ssh version 2

! Configurar linhas VTY para aceitar apenas SSH
R1(config)# line vty 0 15
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit

R1# write memory
```

### Testando SSH do PC

```cmd
ssh -l admin 192.168.1.1
Password: Senha@123
R1#
```

---

## ⚔️ Telnet vs SSH — Comparação de Segurança

| | Telnet | SSH |
|--|--------|-----|
| **Criptografia** | ❌ Nenhuma | ✅ Completa |
| **Porta** | 23 | 22 |
| **Autenticação** | Usuário/senha (texto plano) | Usuário/senha ou chave pública |
| **Visibilidade** | Qualquer sniffer captura tudo | Tráfego é ilegível |
| **Uso recomendado** | ❌ Nunca em produção | ✅ Sempre |
| **Versão** | — | SSHv2 (SSHv1 tem vulnerabilidades) |

---

## 💡 Aprendizados

- **Nunca usar Telnet em produção** — em qualquer análise de tráfego, as credenciais ficam expostas.
- SSH requer hostname + domínio configurados antes de gerar a chave RSA.
- `transport input ssh` nas VTY lines **proíbe Telnet** — apenas SSH é aceito.
- A chave RSA de 2048 bits é o mínimo recomendado; 4096 bits é ideal para ambientes críticos.
- SSH v2 corrigiu várias vulnerabilidades do v1 — sempre usar `ip ssh version 2`.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `Uso do Telnet e SSH.pka` nesta pasta para abrir no Cisco Packet Tracer.
