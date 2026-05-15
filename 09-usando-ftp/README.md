# Lab 09 — Usando Serviços FTP

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Usando serviços FTP.pka`](./Usando%20servi%C3%A7os%20FTP.pka)

---

## 🎯 Objetivo

Utilizar o protocolo **FTP (File Transfer Protocol)** para transferir arquivos entre um cliente e um servidor, observando as portas utilizadas e o processo de autenticação.

---

## 📡 Topologia

```
[PC Cliente] ──── [Switch] ──── [Servidor FTP]
                               192.168.1.100
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **FTP** | Protocolo de transferência de arquivos (porta 21 controle, 20 dados) |
| **Autenticação FTP** | Usuário e senha (em texto plano — não é seguro!) |
| **Modo Ativo vs Passivo** | Como o canal de dados é estabelecido |
| **SFTP / FTPS** | Versões seguras do FTP (com criptografia) |

---

## 🪜 Procedimento realizado

1. Configurado servidor FTP com usuário `cisco` e senha `cisco`
2. No PC cliente, abri o terminal e conectei ao servidor:

```bash
ftp 192.168.1.100
```

3. Realizei as operações:

```ftp
ftp> open 192.168.1.100
Connected to 192.168.1.100.
Name: cisco
Password: cisco
230 Login successful.

ftp> ls
# Lista os arquivos disponíveis

ftp> get arquivo.txt
# Faz download do arquivo

ftp> put meuarquivo.txt
# Faz upload do arquivo

ftp> quit
```

4. Ativei simulação para observar as portas 20 e 21 em uso

---

## ⚠️ FTP e Segurança

| Protocolo | Criptografia | Porta | Recomendado |
|-----------|-------------|-------|-------------|
| FTP | ❌ Nenhuma | 21/20 | ❌ Não usar |
| FTPS | ✅ SSL/TLS | 990 | ⚠️ Legado |
| SFTP | ✅ SSH | 22 | ✅ Sim |

> **⚠️ Atenção:** O FTP transmite usuário, senha e dados em **texto plano**. Qualquer pessoa na rede pode capturar essas informações com um sniffer. Prefira sempre SFTP.

---

## 💡 Aprendizados

- FTP usa **duas conexões TCP**: porta 21 para comandos e porta 20 para transferência de dados.
- No modo **ativo**, o servidor inicia a conexão de dados (problemático com firewalls/NAT).
- No modo **passivo**, o cliente inicia ambas as conexões (mais compatível com NAT).
- SFTP (porta 22) é a alternativa segura — usa SSH para criptografar tudo.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
