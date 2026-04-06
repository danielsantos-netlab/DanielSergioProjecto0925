# SergioDanielProjecto0925

# ATEC // SYSTEM_CORE_2026

Ferramenta de administração e monitorização de sistemas Windows desenvolvida no âmbito do curso de *Gestão de Redes e Sistemas Computacionais (GRSC)* na ATEC — Academia de Formação.

O projeto combina uma interface de linha de comandos em PowerShell com um servidor HTTP local e um dashboard web, permitindo gerir e monitorizar um servidor Windows a partir de uma única plataforma.

---

## Funcionalidades

O sistema está organizado em 10 módulos independentes, acessíveis tanto pela CLI como pelo dashboard web.

### Monitorização
- *Processos e Memória* — listagem completa, top por CPU/RAM, terminação interativa, deteção de processos suspeitos e relatórios de exportação
- *Recursos (CPU / RAM / Disco / Rede)* — snapshot em tempo real, histórico de desempenho, alertas por threshold e monitorização contínua (live mode)

### Sistema
- *Sistema de Ficheiros* — uso de disco por partição, pesquisa de ficheiros grandes, gestão de permissões NTFS, deteção de ficheiros suspeitos e auditoria
- *Serviços e Servidores* — gestão de serviços Windows, monitorização de serviços críticos, configuração de File Server, Print Server e acesso remoto
- *Utilizadores e Grupos* — criação, remoção e ativação/desativação de contas, gestão de grupos, suporte a modo local e modo Active Directory

### Segurança
- *Segurança e Análise* — logins falhados e bem-sucedidos, portas abertas, log de segurança, estado da firewall e auditoria de tarefas agendadas

### Infraestrutura
- *Rede* — adaptadores de rede, conexões ativas, ping, DNS, tabela ARP e tabela de rotas
- *Backup e Recuperação* — backups completos, incrementais e diferenciais, verificação de integridade, agendamento e restauro
- *Configuração de Servidor* — hostname, IP estático, fuso horário, domínio, RDP, DNS e regras de firewall
- *Virtualização (Hyper-V)* — instalação do role, listagem de VMs, criação, gestão de estado, snapshots, exportação e remoção

---

## Arquitetura


ATEC_SYSTEM_CORE_2026/
├── LAUNCHER.bat              # Ponto de entrada — eleva para admin e apresenta o mini-menu
├── MainMenu.ps1              # Menu principal (CLI) com status bar em tempo real
├── Server.ps1                # Servidor HTTP local na porta 8080 (API REST)
├── dashboard.html            # Dashboard web (acedido via http://localhost:8080/dashboard)
├── Config.ps1                # Configuração global, thresholds e funções auxiliares
├── Setup.ps1                 # Setup automático na primeira execução
├── 1_Processes.ps1           # Módulo: Processos e Memória
├── 2_FileSystem.ps1          # Módulo: Sistema de Ficheiros
├── 3_Resources.ps1           # Módulo: Recursos
├── 4_Security.ps1            # Módulo: Segurança
├── 5_Users.ps1               # Módulo: Utilizadores e Grupos
├── 6_Services.ps1            # Módulo: Serviços e Servidores
├── 7_Network.ps1             # Módulo: Rede
├── 8_Backup.ps1              # Módulo: Backup e Recuperação
├── 9_ServerConfig.ps1        # Módulo: Configuração de Servidor
├── 10_Virtualization.ps1     # Módulo: Virtualização (Hyper-V)
├── Logs/                     # Logs diários (sysadmin_YYYY-MM-DD.log)
├── Reports/                  # Relatórios exportados (.txt)
└── Backups/
    ├── Full/
    ├── Incremental/
    └── Differential/


---

## Requisitos

| Componente | Versão mínima |
|---|---|
| Windows Server | 2019 / 2022 / 2025 |
| PowerShell | 5.1 ou superior |
| Permissões | Administrador local |
| Hyper-V | Role instalado ou instalável pelo módulo 10 |
| Active Directory | Detetado automaticamente; fallback para modo local |

---

## Instalação e Execução

1. Copiar todos os ficheiros para uma pasta (ex: C:\ATEC_SYSTEM_CORE_2026).
2. Clicar com o botão direito em LAUNCHER.bat e selecionar *Executar como Administrador*.
3. O launcher copia os ficheiros para C:\Project, cria a estrutura de pastas, define a execution policy e abre o mini-menu.

### Mini-menu do Launcher


[1]  Main Menu           // PowerShell CLI
[2]  Server + Dashboard  // API + Browser
[0]  Exit


A opção [1] abre o menu principal em PowerShell numa nova janela.  
A opção [2] inicia o servidor HTTP na porta 8080 e abre automaticamente o dashboard no browser.

---

## API REST (Server.ps1)

O Server.ps1 expõe uma API REST local em http://localhost:8080. Todos os endpoints devolvem JSON.

| Grupo | Exemplos de endpoints |
|---|---|
| Processos | /api/processes, /api/process/kill, /api/process/suspicious |
| Sistema de Ficheiros | /api/filesystem/disks, /api/filesystem/largefiles, /api/filesystem/permissions |
| Recursos | /api/resources, /api/resources/history, /api/resources/record |
| Segurança | /api/security/ports, /api/security/failedlogins, /api/security/firewall |
| Utilizadores | /api/users, /api/user/create, /api/user/toggle |
| Serviços | /api/services, /api/service/start, /api/services/critical |
| Rede | /api/network, /api/network/ping, /api/network/dns, /api/network/arp |
| Backup | /api/backup/list, /api/backup/run, /api/backup/verify, /api/backup/restore |
| Logs e Relatórios | /api/logs, /api/logs/download, /api/reports, /api/report/generate |

---

## Thresholds Padrão

Os alertas de recursos são configuráveis em Config.ps1 ou diretamente em MainMenu.ps1.

| Recurso | Threshold de alerta |
|---|---|
| CPU | 85% |
| RAM | 80% |
| Disco | 90% |

---

## Contexto Académico

Projeto desenvolvido para a unidade curricular de *Instalar e Parametrizar Sistemas Operativos de Servidor (Plataforma Proprietária)* do curso de nível 5 em *Gestão de Redes e Sistemas Computacionais* na *ATEC — Academia de Formação*, Palmela.

---

## Autor

*Daniel Santos / Sérgio Correia*
