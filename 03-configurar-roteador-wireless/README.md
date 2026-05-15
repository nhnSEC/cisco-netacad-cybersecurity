# Lab 03 — Configurar um Roteador Sem Fio e um Cliente

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Configurar um Roteador sem fio e um cliente.pka`](./Configurar%20um%20Roteador%20sem%20fio%20e%20um%20cliente.pka)

---

## 🎯 Objetivo

Configurar um roteador wireless (sem fio) do zero, definindo o nome da rede (SSID), senha de segurança e conectar um cliente PC sem fio à rede configurada.

---

## 📡 Topologia

```
[Notebook/PC sem fio] )))  (((  [Roteador Wireless] ──── [Internet / Rede Externa]
                         Wi-Fi
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **SSID** | Nome da rede Wi-Fi (Service Set Identifier) |
| **WPA2** | Padrão de segurança Wi-Fi mais utilizado (usa AES) |
| **Canal Wi-Fi** | Frequência usada para transmissão (1, 6 ou 11 evitam sobreposição) |
| **GUI do Roteador** | Interface web de administração (geralmente 192.168.0.1) |
| **Autenticação** | Processo de verificar a senha antes de conceder acesso à rede |

---

## 🪜 Procedimento realizado

1. Acessei a interface de configuração do roteador via navegador (`192.168.0.1`)
2. Configurei o roteador:

**Configurações básicas:**
```
SSID (nome da rede): MinhaRedeWifi
Segurança: WPA2-Personal
Senha: Senha@123
Canal: 6
Banda: 2.4 GHz
```

3. Salvei as configurações e reiniciei o roteador
4. No PC cliente, busquei redes disponíveis
5. Selecionei o SSID configurado e inseri a senha
6. Verifiquei a conexão com `ping` ao gateway

---

## 🔎 O que observei

- Sem SSID visível, o cliente não consegue "ver" a rede — o roteador pode ocultar o SSID por segurança adicional.
- WPA2 com AES é muito mais seguro que WEP ou WPA1 (ambos têm vulnerabilidades conhecidas).
- O canal 6 é padrão por não sofrer interferência dos canais 1 e 11.

---

## 📚 Conceitos de segurança Wi-Fi

| Protocolo | Status | Vulnerabilidade |
|-----------|--------|-----------------|
| WEP | ❌ Obsoleto | Quebrado em segundos com ferramentas simples |
| WPA | ⚠️ Fraco | Vulnerável ao ataque TKIP |
| WPA2 (AES) | ✅ Recomendado | Padrão atual seguro |
| WPA3 | ✅ Mais recente | Proteção contra ataques de dicionário |

---

## 💡 Aprendizados

- A configuração de um roteador wireless envolve tanto a camada física (frequência, canal) quanto as camadas de segurança (autenticação, criptografia).
- Nunca deixar o roteador com as credenciais padrão de fábrica — é a primeira coisa que um atacante tenta.
- O SSID oculto não é segurança real — ferramentas de análise de rede conseguem detectar redes ocultas.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
