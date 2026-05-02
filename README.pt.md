# 🌐 NetPractice

[Read in English](README.md)

> Um projeto abrangente de configuração de redes do **currículo 42**, que domina o endereçamento TCP/IP através de 10 níveis práticos progressivos.

---

## 📝 Descrição

**NetPractice** é um projeto prático de redes onde resolves problemas de configuração semelhantes ao mundo real, usando uma interface de simulação no browser. Cada nível apresenta uma topologia de rede com problemas — incluindo hosts, switches e routers — e o teu objetivo é configurar corretamente os endereços IP, as máscaras de sub-rede e as tabelas de encaminhamento para que todos os objetivos de comunicação sejam cumpridos.

O simulador fornece **feedback imediato** sobre configurações incorretas, tornando-o uma excelente ferramenta de aprendizagem para perceber como os pacotes circulam nas redes.

---

## 🚀 Início Rápido

### Pré-requisitos

- Um browser moderno (Chrome, Firefox, Safari, Edge)
- Python 3.x (para executar o servidor local)
- As tuas credenciais de acesso à intranet 42

### Executar o Simulador

1. **Descarrega os ficheiros do projeto** a partir da página do projeto 42 e extrai-os.

2. **Navega até ao diretório do projeto** e executa o script de arranque:
   ```bash
   bash run.sh
   ```

   Se `run.sh` não funcionar, inicia o servidor manualmente:
   ```bash
   python3 -m http.server 49242
   ```

3. **Abre o browser** e navega para:
   ```
   http://localhost:49242
   ```

4. **Introduz o teu login 42** para gerar configurações personalizadas para cada nível.

---

## 📊 Visão Geral dos Níveis

| Nível | Conceito | Dificuldade | Foco |
|:-----:|---------|:----------:|-------|
| **1** | Endereçamento IP Básico | ⭐ | Dois pares de hosts isolados em redes separadas |
| **2** | Máscaras de Sub-rede CIDR | ⭐ | Introdução à notação `/30`, `/29`, `/28` |
| **3** | Switch e Sub-rede Partilhada | ⭐ | Um switch a ligar múltiplos hosts |
| **4** | Router com Switch | ⭐⭐ | Interface de router numa rede com switch |
| **5** | Gateway Predefinido | ⭐⭐ | Hosts a encaminhar para redes externas via gateway |
| **6** | Encaminhamento para a Internet | ⭐⭐ | Rota predefinida (`0.0.0.0/0`) para a Internet |
| **7** | Encaminhamento Estático (2 Routers) | ⭐⭐⭐ | Comunicação entre sub-redes através de routers |
| **8** | Múltiplos Routers + NAT | ⭐⭐⭐ | Configuração de NAT/gateway com múltiplos routers |
| **9** | Múltiplas Sub-redes Complexas | ⭐⭐⭐ | Múltiplos routers, sub-redes e acesso à Internet |
| **10** | Integração de Topologia Completa | ⭐⭐⭐⭐ | 4 hosts, 2 routers, 1 switch, Internet — rede completa |

---

## 📸 Soluções Visuais

### Nível 1 — Endereçamento IP Básico
![Nível 1](imgs/level1.png)

### Nível 2 — Máscaras de Sub-rede CIDR
![Nível 2](imgs/level2.png)

### Nível 3 — Switch com Múltiplos Hosts
![Nível 3](imgs/level3.png)

### Nível 4 — Router com Switch
![Nível 4](imgs/level4.png)

### Nível 5 — Gateway Predefinido
![Nível 5](imgs/level5.png)

### Nível 6 — Encaminhamento para a Internet
![Nível 6](imgs/level6.png)

### Nível 7 — Encaminhamento Estático com Dois Routers
![Nível 7](imgs/level7.png)

### Nível 8 — Múltiplos Routers + Internet
![Nível 8](imgs/level8.png)

### Nível 9 — Topologia Complexa com Múltiplas Sub-redes
![Nível 9](imgs/level9.png)

### Nível 10 — Topologia de Rede Completa
![Nível 10](imgs/level10.png)

---

## 🛠️ Como Resolver

### Abordagem Passo a Passo

1. **Lê a topologia** — Identifica todos os hosts, switches, routers e a Internet.

2. **Analisa os objetivos** — O lado direito da interface mostra que comunicações devem ser possíveis.

3. **Identifica as sub-redes** — Determina quais os dispositivos que devem estar na mesma rede com base na topologia.

4. **Configura os endereços IP**:
   - Cada dispositivo na mesma ligação física deve estar na mesma sub-rede.
   - Usa uma máscara de sub-rede adequada ao número de dispositivos nessa ligação.
   - Atribui IPs sequenciais dentro do intervalo válido de hosts.

5. **Define os gateways predefinidos** — Os hosts precisam de saber qual a interface do router a usar para alcançar outras redes.

6. **Configura as tabelas de encaminhamento** — Os routers precisam de entradas para todas as redes de destino que conseguem alcançar.

7. **Valida** — Clica em **Check again** e revê os registos. Corrige os problemas e tenta de novo.

8. **Exporta a configuração** — Clica em **Get my config** e guarda o ficheiro antes de avançar para o nível seguinte.

### Regras Fundamentais

| Regra | Exemplo |
|-------|---------|
| **Mesma ligação física = mesma sub-rede** | Se o Host A e o Router R1 estão no mesmo switch, ambos devem ter IPs na mesma rede `/24` |
| **Interfaces do router** | Cada interface do router precisa de um endereço IP na sub-rede dos dispositivos a que se liga |
| **Gateway predefinido** | O gateway de um host é **sempre** o IP da interface do router na mesma rede |
| **Destino na tabela de encaminhamento** | Deve ser um endereço de rede (ex.: `192.168.2.0/24`, não um IP de host) |
| **Próximo salto** | Deve ser o IP de uma interface de router diretamente ligada |
| **Rota para a Internet** | Usa `0.0.0.0/0` para representar todo o tráfego externo |

---

## 🧠 Conceitos Fundamentais

### Endereçamento TCP/IP

- **Estrutura do endereço IPv4** — 32 bits divididos em 4 octetos (ex.: `192.168.1.5`)
- **Máscara de sub-rede** — Determina quais os bits que identificam a rede vs. o host
- **Notação CIDR** — Abreviatura para máscaras de sub-rede (ex.: `/24` = `255.255.255.0`)
- **Endereço de rede** — Primeiro IP de uma sub-rede; não pode ser atribuído a um host
- **Endereço de broadcast** — Último IP de uma sub-rede; usado para mensagens a toda a rede
- **Intervalo válido de hosts** — Todos os IPs entre os endereços de rede e de broadcast

### Dispositivos de Rede

| Dispositivo | Camada | Função | Exemplo |
|-------------|--------|--------|---------|
| **Host** | L3 | Dispositivo terminal que envia/recebe tráfego | Computador, servidor, impressora |
| **Switch** | L2 | Liga dispositivos na mesma rede | Reencaminha tramas por endereço MAC |
| **Router** | L3 | Liga redes diferentes | Reencaminha pacotes por endereço IP |
| **Internet** | L3 | Rede global de redes | Representada por `0.0.0.0/0` |

### Fundamentos de Encaminhamento

- **Encaminhamento estático** — O administrador configura as rotas manualmente (usado neste projeto)
- **Encaminhamento dinâmico** — Os routers descobrem rotas automaticamente (OSPF, BGP, etc.)
- **Entrada na tabela de encaminhamento** — `[Rede de Destino] → [IP do Próximo Salto]`
- **Correspondência de prefixo mais longo** — Os routers selecionam a rota correspondente mais específica (mais longa)
- **Rota predefinida** — Rota de captura para qualquer tráfego que não corresponda a uma entrada específica

---

## 📐 Tabela de Referência CIDR

| CIDR | Máscara de Rede | IPs Totais | Hosts Utilizáveis | Uso Comum |
|:----:|-----------------|:----------:|:-----------------:|-----------|
| `/31` | `255.255.255.254` | 2 | 2* | Ligações ponto a ponto (router a router) |
| `/30` | `255.255.255.252` | 4 | 2 | Redes pequenas, ligações série |
| `/29` | `255.255.255.248` | 8 | 6 | Pequeno escritório, filial |
| `/28` | `255.255.255.240` | 16 | 14 | Rede departamental |
| `/27` | `255.255.255.224` | 32 | 30 | Edifício, piso |
| `/26` | `255.255.255.192` | 64 | 62 | Grande escritório |
| `/25` | `255.255.255.128` | 128 | 126 | Edifício de campus |
| `/24` | `255.255.255.0` | 256 | 254 | Pequena organização, sub-rede |
| `/23` | `255.255.254.0` | 512 | 510 | Organização |
| `/22` | `255.255.252.0` | 1024 | 1022 | Múltiplos departamentos |

*Para `/31`, ambos os IPs são utilizáveis (RFC 3021 — ligações ponto a ponto)

### Cálculo Rápido de CIDR

Para encontrar o **número de hosts utilizáveis** a partir de uma notação CIDR:
```
Hosts Utilizáveis = 2^(32 - CIDR) - 2
```

Exemplos:
- `/24`: 2^(32-24) - 2 = 2^8 - 2 = 256 - 2 = **254 hosts**
- `/28`: 2^(32-28) - 2 = 2^4 - 2 = 16 - 2 = **14 hosts**
- `/30`: 2^(32-30) - 2 = 2^2 - 2 = 4 - 2 = **2 hosts**

---

## 🔍 Guia de Resolução de Problemas

### Os Pacotes Não Chegam ao Destino?

Segue esta lista de verificação por ordem:

#### 1. **Verifica a Configuração do Host**
```
✓ O IP do host está dentro da sub-rede definida pela sua máscara?
✓ A máscara do host está correta?
✓ O host tem um gateway predefinido configurado?
```

**Solução:** Recalcula o intervalo da sub-rede. Usa uma calculadora de sub-redes se tiveres dúvidas.

#### 2. **Verifica a Conectividade com o Gateway**
```
✓ O IP do gateway existe numa interface do router?
✓ O IP do gateway está na mesma sub-rede que o host?
✓ A interface do router está ativa e configurada?
```

**Solução:** Certifica-te de que a interface do router tem um IP na mesma sub-rede que o host.

#### 3. **Verifica o Encaminhamento no Router de Origem**
```
✓ O router tem uma rota para a rede de destino?
✓ A rota aponta para um próximo salto válido?
✓ O próximo salto é alcançável através de uma interface diretamente ligada?
```

**Solução:** Adiciona uma entrada na tabela de encaminhamento para a rede de destino.

#### 4. **Verifica o Encaminhamento nos Routers Intermédios**
```
✓ Todos os routers entre a origem e o destino têm as rotas necessárias?
✓ Cada rota aponta para o próximo router no caminho?
✓ Os routers estão devidamente ligados?
```

**Solução:** Traça o caminho e certifica-te de que cada router sabe como alcançar tanto a origem como o destino.

#### 5. **Verifica o Caminho de Retorno** ⚠️ Problema Mais Comum
```
✓ A rede de destino tem uma rota de volta para a origem?
✓ A rota de retorno está correta?
```

**Solução:** Os routers próximos do destino devem ter rotas de volta para a rede de origem. Isto é muitas vezes esquecido!

### Problemas Comuns

| Problema | Causa | Solução |
|----------|-------|---------|
| "Host unreachable" | Sem rota no router | Adiciona rota à tabela de encaminhamento |
| "Network unreachable" | Gateway ou máscara incorretos | Verifica se o host está na mesma sub-rede que o gateway |
| Comunicação assimétrica | Rota de retorno em falta | Adiciona rota de volta para a rede de origem no router do lado do destino |
| "Packet dropped" | Interface não configurada | Atribui IP a todas as interfaces do router |
| Internet inacessível | Sem rota predefinida | Adiciona rota `0.0.0.0/0` a apontar para o gateway do ISP |

---

## 📦 Estrutura do Projeto

```
.
├── README.md              # Ficheiro em inglês
├── README.pt.md           # Este ficheiro
├── level1.json            # Configuração do Nível 1 (exportada)
├── level2.json            # Configuração do Nível 2 (exportada)
├── level3.json            # Configuração do Nível 3 (exportada)
├── level4.json            # Configuração do Nível 4 (exportada)
├── level5.json            # Configuração do Nível 5 (exportada)
├── level6.json            # Configuração do Nível 6 (exportada)
├── level7.json            # Configuração do Nível 7 (exportada)
├── level8.json            # Configuração do Nível 8 (exportada)
├── level9.json            # Configuração do Nível 9 (exportada)
└── level10.json           # Configuração do Nível 10 (exportada)
```

---

## 📚 Recursos

### Materiais de Aprendizagem

- **[Cisco Networking Basics — TCP/IP](https://www.cisco.com/c/en/us/solutions/small-business/resource-center/networking/networking-basics.html)** — Conceitos fundamentais de TCP/IP
- **[Professor Messer — Subnetting](https://www.professormesser.com/network-plus/n10-008/n10-008-video/classful-subnetting-n10-008/)** — Explicação clara de sub-redes
- **[RFC 791 — Internet Protocol](https://www.rfc-editor.org/rfc/rfc791)** — Especificação oficial do IPv4
- **[RFC 3021 — Using 31-Bit Prefixes on IPv4 Point-to-Point Links](https://www.rfc-editor.org/rfc/rfc3021)** — Porque é que `/31` funciona

### Ferramentas

- **[Subnet Calculator](https://www.subnet-calculator.com/)** — Cálculos interativos de CIDR/sub-rede
- **[ipcalc](http://jodies.de/ipcalc)** — Calculadora IP para linha de comandos
- **[Cisco IOS Routing Fundamentals](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html)** — Conceitos de tabela de encaminhamento

### Wikipédia

- **[CIDR — Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)**
- **[Subnet — Subnetwork](https://en.wikipedia.org/wiki/Subnetwork)**
- **[Modelo OSI](https://en.wikipedia.org/wiki/OSI_model)**
- **[Longest Prefix Match](https://en.wikipedia.org/wiki/Longest_prefix_match)**

---

## ⚙️ Notas de Avaliação

Durante a **avaliação entre pares**, ser-te-á pedido que resolvas **3 níveis aleatórios** ao vivo dentro de um limite de tempo. Pontos importantes:

- ✅ **Não são permitidas ferramentas externas**, exceto uma calculadora simples (ex.: `bc` ou a calculadora do sistema)
- ✅ **Todos os ficheiros de configuração** devem estar na raiz do repositório (`level1.json` a `level10.json`)
- ✅ **As capturas de ecrã** (pasta imgs) são opcionais, mas úteis para referência
- ✅ **Este README** serve de guia de estudo durante as defesas
- ✅ **Compreensão > memorização** — Os avaliadores podem pedir-te que expliques as tuas escolhas de configuração

---
