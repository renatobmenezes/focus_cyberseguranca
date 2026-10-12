# Investigação Forense de Logs e Inteligência de Ameaças

**Status do laboratório:** Concluído
**Nível:** Iniciante / Intermediário
**Área:** Cibersegurança, análise forense e inteligência de ameaças

## 1. Objetivo do projeto

O projeto teve como objetivo analisar registros de acesso de um servidor Linux para identificar atividades suspeitas, localizar informações codificadas, recuperar mensagens ocultas e investigar endereços IP relacionados às tentativas de acesso.

Durante o laboratório, foram utilizados comandos de terminal para filtrar registros, o CyberChef para decodificar informações e o VirusTotal para consultar dados relacionados aos endereços IP identificados.

## 2. Ferramentas utilizadas

* **Terminal (PowerShell):** criação de diretórios, extração de arquivos e pesquisa de informações nos logs.
* **CyberChef:** decodificação de dados em Base64 e filtragem de conteúdo por expressão regular.
* **VirusTotal:** consulta de informações de inteligência de ameaças relacionadas a endereços IP.
* **Arquivo `access.log`:** registro de acessos utilizado para identificar requisições suspeitas.
* **Arquivo `encodedflag.txt`:** arquivo de texto utilizado na investigação da mensagem codificada.

## 3. Etapas da investigação

### Missão 1 — Preparação do ambiente e análise dos logs

Inicialmente, foi criado um diretório para o laboratório e extraído o arquivo compactado `loganalysis-1695809155170.zip`.

Em seguida, foi utilizado o comando `Select-String` no PowerShell para pesquisar ocorrências do padrão `==` no arquivo `access.log`, com o objetivo de localizar requisições que poderiam conter dados codificados em Base64.

A análise permitiu identificar um endereço IP associado à tentativa de extração de uma flag codificada.

### Missão 2 — Decodificação dos artefatos no CyberChef

Na segunda etapa, o CyberChef foi utilizado para analisar duas evidências distintas.

A primeira consistiu em uma sequência extraída do log, que foi submetida à operação `From Base64` para revelar a flag.

A segunda envolveu o conteúdo do arquivo `encodedflag.txt`. Após a aplicação de `From Base64` e de uma filtragem por expressão regular para localizar um endereço MAC, foi identificada uma sequência com o formato de um endereço físico de rede.

### Missão 3 — Investigação dos endereços IP no VirusTotal

Por fim, foram consultadas informações relacionadas aos endereços IP identificados durante a análise.

A investigação buscou verificar a localização geográfica e a organização provedora de conectividade associadas a um dos endereços, além de reunir informações que auxiliassem na compreensão da atividade suspeita.

## 4. Perguntas e respostas do laboratório

### 1. Qual é o endereço IP do atacante que tentou extrair a flag Base64 no log?

**Resposta:** `212.14.17.145`

**Ferramentas utilizadas:** Terminal, PowerShell, `Select-String` e arquivo `access.log`.

**Procedimento:** Foi realizada uma pesquisa pelo padrão `==` no arquivo de log. A análise da requisição suspeita permitiu identificar o endereço IP associado à tentativa de extração da flag.

### 2. Qual é a palavra ou frase secreta revelada ao aplicar a receita From Base64 no CyberChef?

**Resposta:** `THM{CYBERCHEF_WIZARD}`

**Ferramenta utilizada:** CyberChef.

**Procedimento:** A sequência codificada extraída do log foi inserida no campo Input e processada com a operação `From Base64`. O resultado revelou a flag secreta.

### 3. De qual país e empresa de internet partiu o IP `54.36.115.221`, que varreu o arquivo oculto `.env`?

**Resposta:** França — OVH SAS.

**Ferramenta utilizada:** VirusTotal.

**Procedimento:** O endereço IP foi consultado na plataforma para verificar informações sobre sua localização e a organização de conectividade associada. O resultado registrado durante a investigação apontou a França e a OVH SAS.

### 4. Qual mensagem secreta de sucesso foi descriptografada do arquivo `http://encodedflag.txt`?

**Resposta obtida:** `08-2E-9A-4B-7F-61`

**Ferramentas utilizadas:** CyberChef, `From Base64` e expressão regular para identificação de endereço MAC.

**Procedimento:** O conteúdo do arquivo `encodedflag.txt` foi processado no CyberChef. Após a decodificação em Base64, foi aplicada uma expressão regular para localizar uma sequência com o formato de um endereço MAC. O resultado identificado foi `08-2E-9A-4B-7F-61`.

## 5. Conclusão

O laboratório permitiu praticar etapas fundamentais de uma investigação inicial em cibersegurança: preparação de um ambiente de análise, pesquisa em registros de acesso, identificação de requisições suspeitas, decodificação de informações e consulta de dados de inteligência de ameaças.

A atividade também demonstrou como ferramentas simples podem ser combinadas para investigar evidências digitais. O terminal foi utilizado para localizar dados relevantes nos logs, o CyberChef para interpretar sequências codificadas e o VirusTotal para consultar informações sobre endereços IP.

Como aprendizado, destaca-se a importância de analisar os resultados com cuidado, diferenciar codificação de criptografia e validar cada evidência antes de concluir que uma sequência representa uma flag, senha ou mensagem de sucesso.

