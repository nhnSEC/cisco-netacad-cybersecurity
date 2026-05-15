# Lab 10 — Use o Comando ipconfig

**Módulo:** Redes Básicas | **Plataforma:** Cisco Packet Tracer  
**Arquivo:** [`Use o comando ipconfig.pka`](./Use%20o%20comando%20ipconfig.pka)

---

## 🎯 Objetivo

Utilizar o comando `ipconfig` para verificar, renovar e liberar configurações de rede em um PC Windows, entendendo cada informação exibida e sua utilidade no diagnóstico de problemas.

---

## 🪜 Procedimento realizado

### Verificar configuração atual
```cmd
ipconfig
```
Saída típica:
```
Ethernet adapter Ethernet0:
   Connection-specific DNS Suffix  . :
   IPv4 Address. . . . . . . . . . . : 192.168.1.10
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.1.1
```

### Ver informações detalhadas (inclui MAC e DNS)
```cmd
ipconfig /all
```
Saída adicional:
```
   Physical Address. . . . . . . . . : 00-1A-2B-3C-4D-5E
   DHCP Enabled. . . . . . . . . . . : Yes
   DHCP Server . . . . . . . . . . . : 192.168.1.1
   DNS Servers . . . . . . . . . . . : 8.8.8.8
   Lease Obtained. . . . . . . . . . : seg, 12 mai 2026
   Lease Expires . . . . . . . . . . : ter, 13 mai 2026
```

### Liberar IP (DHCP)
```cmd
ipconfig /release
```
> Remove o IP atual — o PC fica sem endereço IP até renovar.

### Renovar IP (solicita novo lease ao DHCP)
```cmd
ipconfig /renew
```

### Limpar cache DNS
```cmd
ipconfig /flushdns
```
> Útil quando um site muda de IP e o PC ainda está usando o IP antigo em cache.

---

## 🔍 O que cada campo significa

| Campo | Significado |
|-------|-------------|
| **IPv4 Address** | Endereço IP do computador nessa rede |
| **Subnet Mask** | Define o tamanho da rede (ex: /24 = 254 hosts) |
| **Default Gateway** | IP do roteador — porta de saída para outras redes |
| **Physical Address** | Endereço MAC da placa de rede |
| **DHCP Enabled** | Se o IP foi obtido automaticamente (Yes) ou é estático (No) |
| **DNS Servers** | Servidores que traduzem nomes em IPs |
| **Lease Obtained/Expires** | Quando o IP foi concedido e quando expira |

---

## 🩺 ipconfig como ferramenta de diagnóstico

| Problema | O que verificar |
|----------|----------------|
| Sem internet | Gateway configurado? DNS correto? |
| IP `169.254.x.x` | DHCP falhou — IP autoatribuído (APIPA) |
| Site não abre | `ipconfig /flushdns` pode resolver cache desatualizado |
| IP errado | Verificar se DHCP está ativo ou se foi configurado estático errado |

---

## 💡 Aprendizados

- `ipconfig /all` deve ser o primeiro comando em qualquer diagnóstico de rede.
- IP `169.254.x.x` significa que o PC não conseguiu contato com o servidor DHCP — é um sinal de alerta.
- O `flushdns` é especialmente útil em ambientes de desenvolvimento ou após migrações de domínio.

---

## 📎 Arquivo do Lab

> Coloque o arquivo `.pka` nesta pasta para abrir no Cisco Packet Tracer.
