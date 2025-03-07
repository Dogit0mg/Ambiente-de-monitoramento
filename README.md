# Projeto 4 - Ambiente de Monitoramento e Resposta com EDR e Malware Personalizado

## Objetivo:
Criar um laboratório virtual utilizando VMware para simular um ambiente real de ataque e resposta. O projeto visa a implementação de técnicas de invasão e monitoramento, utilizando diversas ferramentas de segurança para gerar, controlar e identificar ações maliciosas em um ambiente controlado.

## Tecnologias Utilizadas:
- **Ubuntu Server** – Sistema operacional Linux para gerenciamento de serviços e execução de ferramentas.
- **Windows 10** – Sistema operacional alvo do projeto.
- **VMware** – Plataforma de virtualização para criação e gerenciamento das máquinas virtuais.
- **LimaCharlie EDR** – Ferramenta de detecção e resposta a incidentes para monitorar o sistema Windows.
- **Sysmon** – Utilizado em conjunto com LimaCharlie para agrupar e analisar informações do sistema.
- **OpenSSH** – Para acesso remoto à máquina Linux.
- **Sliver-server** – Plataforma para geração e gerenciamento de payloads e sessões C2.
- **Python3** – Para criar um servidor temporário que transfere o malware para o alvo.

## Descrição do Projeto:

### Fase 1 - Criação do Laboratório
- **Criação das Máquinas Virtuais:**
  - Utilização do [**VMware**](https://www.vmware.com/) para criar e configurar as máquinas virtuais com [**Ubuntu Server**](https://ubuntu.com/download/server) e **Windows 10**.
  - Configuração da rede virtual, com atenção especial à atribuição de um IP estático para a máquina Ubuntu, garantindo comunicação confiável entre os sistemas.
  
- **Instalação e Configuração de Ferramentas Básicas:**
  - **Ubuntu Server:**
    - Instalação do **OpenSSH** para permitir acesso remoto seguro a partir da máquina local.
  - **Windows 10:**
    - Desativação do **Windows Firewall** por meio da alteração de chaves de registro, a fim de facilitar o processo de invasão.
    - Instalação do **Sysmon64** para coletar logs detalhados do sistema.
    - Instalação do sensor do **LimaCharlie EDR**, integrando-o ao Sysmon para centralizar a coleta e análise dos logs do sistema.

### Fase 2 - Preparação para o Ataque
- **Conexão e Gerenciamento Remoto:**
  - Estabelecimento de conexão via SSH, a partir da máquina local, para a máquina Ubuntu.
  - Instalação e configuração do **Sliver-server** na máquina Ubuntu, preparando o ambiente para a criação de payloads e o gerenciamento das sessões C2.
  
- **Geração do Payload e Criação da Sessão C2:**
  - Utilização do **Sliver** para criar um payload customizado que, ao ser executado no sistema alvo (Windows 10), estabelece uma conexão reversa (C2).
  
- **Transferência do Malware:**
  - Criação de um servidor temporário utilizando **Python3** na máquina Ubuntu.
  - Transferência do arquivo do malware para o PC alvo (Windows 10) por meio deste servidor.

### Fase 3 - Execução do Exploit e Monitoramento
- **Iniciação do Ataque:**
  - Execução do arquivo malicioso na máquina Windows 10 para ativar a sessão C2 e iniciar a comunicação com o Sliver-server.
  
- **Comandos utilizados para teste da conexão:**
  - Uma vez estabelecida a conexão, foram executados comandos de monitoramento e controle, tais como:
    - `ps -T`: Listagem dos processos e threads em execução.
    - `netstat`: Visualização das conexões de rede ativas.
    - `pwd`: Exibição do diretório atual.
    - `info`: Coleta de informações detalhadas do sistema.
    - `whoami`: Identificação do usuário atual.
    - `getprivs`: Comando para verificar os privilégios do usuário infectado.
  
- **Coleta de Evidências e Monitoramento:**
  - Foi utilizado o comando **procdump** para extrair informações e criar dumps de processos críticos, criando um alerta de "SENSITIVE_PROCESS_ACCESS" na paltaforma LimaCharlie.
  - Análise dos logs coletados pelo **LimaCharlie EDR** e **Sysmon**, permitindo a identificação das atividades do malware.
  - Criação de alertas no LimaCharlie para avisar quando arquivos sensíveis fossem acessados na máquina Windows, demonstrando a eficácia do monitoramento em tempo real.

## Habilidades Desenvolvidas:
- **Virtualização e Gerenciamento de Ambientes:** Criação e configuração de laboratórios virtuais com VMware.
- **Configuração de Rede:** Atribuição de IP estático e gerenciamento de comunicação entre máquinas virtuais.
- **Administração de Sistemas:** Instalação e configuração de serviços no Ubuntu Server (OpenSSH) e Windows 10 (desativação do firewall, instalação de Sysmon e sensor LimaCharlie).
- **Segurança Ofensiva:** Criação e execução de payloads maliciosos utilizando Sliver e Python3 para transferência e execução do malware.
- **Monitoramento e Resposta a Incidentes:** Utilização de ferramentas EDR (LimaCharlie) e Sysmon para coleta, análise e alerta de atividades maliciosas.
- **Automação e Scripting:** Uso de Python3 para a criação de um servidor temporário, além da automação de comandos e execução de exploits.

---

## Conclusão:
Este projeto demonstra a integração de diversas ferramentas e técnicas para a criação de um ambiente de ataque controlado e o monitoramento em tempo real de atividades maliciosas. Através da combinação de virtualização, ferramentas de EDR e a utilização de payloads customizados, foi possível simular um cenário de invasão e implementar medidas de detecção e resposta, contribuindo significativamente para o aprimoramento das habilidades em segurança ofensiva e defensiva.
