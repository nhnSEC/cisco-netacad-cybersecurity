# Lab 05 — Criar uma LAN

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Criar uma LAN.pka`](./Criar%20uma%20LAN.pka)

---

## 🎯 Objetivo

Construir uma rede local (LAN) do zero no Packet Tracer, conectando múltiplos dispositivos a um switch, configurando endereçamento IP estático e verificando conectividade entre todos os hosts.

---

## 📡 Topologia construída

```
        [PC1] 192.168.1.10
           │
        [PC2] 192.168.1.11
           │
     [Switch 2960] ──── [PC3] 192.168.1.12
           │
        [PC4] 192.168.1.13
           │
     (Cabo UTP Cat5e — porta FastEthernet)
```

---

## 🔍 Conceitos abordados

| Conceito | Descrição |
|----------|-----------|
| **LAN** | Rede local — dispositivos na mesma sub-rede |
| **Switch** | Dispositivo L2 que encaminha quadros pelo endereço MAC |
| **Endereçamento IP** | Cada host precisa de IP único na mesma sub-rede |
| **Máscara de sub-rede** | Define qual parte do IP é rede e qual é host |
| **Ping** | Ferramenta de diagnóstico que testa alcançabilidade |
| **Tabela MAC** | Switch aprende endereços MAC e os associa a portas |

---

## 🪜 Procedimento realizado

1. Adicionei ao canvas: 1 Switch Cisco 2960 + 4 PCs
2. Conectei cada PC ao switch com cabo **UTP direto** (porta FastEthernet)
3. Configurei o IP em cada PC manualmente:

**PC1:**
```
IP: 192.168.1.10
Máscara: 255.255.255.0
Gateway: (não necessário em LAN simples)
```

**PC2:**
```
IP: 192.168.1.11
Máscara: 255.255.255.0
```

**PC3:**
```
IP: 192.168.1.12
Máscara: 255.255.255.0
```

**PC4:**
```
IP: 192.168.1.13
Máscara: 255.255.255.0
```

4. Testei conectividade com `ping` entre todos os pares
5. Verifiquei a tabela MAC do switch com:
```
Switch# show mac address-table
```

---

## 🔎 O que observei

- O switch aprende os endereços MAC automaticamente quando o primeiro frame é enviado.
- Antes de aprender o MAC de destino, o switch faz **flood** (envia para todas as portas) — depois usa a tabela para enviar apenas para a porta correta.
- Todos os PCs na mesma sub-rede (`192.168.1.0/24`) se comunicam **diretamente**, sem precisar de roteador.

---

## 📚 Sub-rede /24 explicada

```
Endereço de rede: 192.168.1.0
Máscara:         255.255.255.0  (ou /24)
Primeiro host:   192.168.1.1
Último host:     192.168.1.254
Broadcast:       192.168.1.255
Total de hosts:  254
```

---

## 💡 Aprendizados

- Um switch **não precisa de configuração de IP** para funcionar em L2 — mas tem um IP de gerenciamento opcional.
- A máscara `/24` é a mais comum em redes domésticas e pequenas empresas.
- Se dois PCs tiverem o **mesmo IP**, nenhum consegue se comunicar corretamente (conflito de IP).
- O comando `ping 192.168.1.11` no terminal do PC testa a camada 3; o switch opera na camada 2.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
