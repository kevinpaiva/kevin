# Solar Energy Monitoring System - Security Overview

## Slide 1: Contextualização da Segurança

**Ambiente de Aplicação:**
- Sistema solar residencial com dois Arduinos (Sun Block e Loop Grid)
- Monitoramento técnico e estimativa de orçamento via site/aplicativo
- Comunicação entre clientes, técnicos e sistema em tempo real

**Superfícies de risco:**
- Hardware (Arduinos e instalações físicas)
- Interface web e aplicativo
- Dados dos usuários e relatórios técnicos

## Slide 2: Possíveis Vulnerabilidades

1. **Acesso físico aos Arduinos** – risco de manipulação ou desligamento indevido
2. **Interceptação de dados via Wi-Fi** – especialmente durante transmissão de relatórios
3. **Injeção de comandos maliciosos no Arduino** – via atualizações ou falhas de autenticação
4. **Phishing ou uso indevido da interface cliente/técnico**
5. **Ausência de autenticação robusta no site/aplicativo** – invasões e vazamentos
6. **Fator humano** (erro/sabotagem sob o sistema em implementação)

## Slide 3: Políticas de Segurança

1. **Autenticação em duas etapas (2FA)** (usuário e senha + token) para técnicos e administradores
2. **Firewall físico e lógico** nos gateways de rede que conectam os Conversores de Energia
3. **Controle de acesso baseado em função (RBAC)** para técnicos e usuários no sistema web/app
4. **Timeout de sessão inativa** após 5 minutos sem atividade
5. **Backup criptografado diário** dos dados sensíveis, armazenados fora do servidor de produção
6. **Acompanhamento da instalação** check entre o orçamento, relatório técnico e efetiva instalação

## Slide 4: Redundância e Contingência

**Plano de redundância:**
- Arduino secundário em modo stand-by para cada função (Sun Block e Loop Grid)
- Armazenamento em nuvem redundante (ex: AWS S3 ou Google Drive com criptografia)

**Plano de contingência:**
- Aplicativo funcional offline (modo leitura para técnicos)
- Logs locais nos Arduinos, exportáveis via Bluetooth em caso de falha de rede
- Manual técnico digital disponível em PDF para instalação emergencial

## Slide 5: Camadas de Segurança Implementadas

1. **Camada Física:** Caixa selada anti-violação para os Arduinos + lacres inteligentes
2. **Camada de Rede:** Criptografia WPA2/WPA3 nas conexões Wi-Fi dos Conversores
3. **Camada de Monitoramento:** Logs automáticos com alertas de acessos fora do padrão
4. **Site hospedado** em estruturas com certificados SSL, proteção contra DDoS

## Slide 6: Uso de Criptografia

**Onde será usada:**
- Transmissão de dados entre Conversor e servidor (HTTPS/TLS 1.3)
- Armazenamento de relatórios técnicos e dados do cliente
- Backup diário na nuvem

**Justificativa:**
- Garante sigilo dos dados sem comprometer a performance
- Protege contra espionagem industrial e concorrência desleal

**Algoritmo escolhido:**
- AES-128 em modo GCM para arquivos
- SHA-256 para hashes de senha
- Equilíbrio ideal entre segurança e processamento nos dispositivos embarcados
