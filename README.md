# Manual Completo de Comandos e Conceitos do Linux

**Data:** 21 de Setembro de 2026
**Versão:** 2.0
**Objetivo:** Referência formal, didática e completa sobre comandos e conceitos fundamentais do sistema operacional Linux

---

## Sumário

1. [Monitoramento de Recursos do Sistema](#1-monitoramento-de-recursos-do-sistema)
2. [Identificação e Informações do Sistema](#2-identificação-e-informações-do-sistema)
3. [Navegação e Manipulação de Arquivos e Diretórios](#3-navegação-e-manipulação-de-arquivos-e-diretórios)
4. [Gerenciamento de Pacotes](#4-gerenciamento-de-pacotes)
5. [Controle do Sistema e Gerenciamento de Serviços](#5-controle-do-sistema-e-gerenciamento-de-serviços)
6. [Rastreamento e Depuração de Processos](#6-rastreamento-e-depuração-de-processos)
7. [Gerenciamento de Boot e Agendamento](#7-gerenciamento-de-boot-e-agendamento)
8. [Monitoramento de Disco, Sessões e Logs](#8-monitoramento-de-disco-sessões-e-logs)
9. [Data, Hora e Hardware](#9-data-hora-e-hardware)
10. [O Sistema de Arquivos Virtual](#10-o-sistema-de-arquivos-virtual)
11. [Gerenciamento de Módulos do Kernel](#11-gerenciamento-de-módulos-do-kernel)
12. [Atualização de Kernel](#12-atualização-de-kernel)
13. [Gerenciamento de Usuários e Grupos](#13-gerenciamento-de-usuários-e-grupos)

---

## 1. Monitoramento de Recursos do Sistema

### `free`
**Resumo:** Exibe a quantidade de memória física (RAM) e de troca (swap) livre e utilizada no sistema.
**Exemplos:**
~~~bash
# Exibe a memória em formato legível para humanos (KB, MB, GB)
free -h

# Exibe apenas a linha de memória total
free -h | grep Mem

# Atualiza a exibição a cada 2 segundos (similar ao top)
free -s 2

# Exibe em bytes (valor exato)
free -b

# Exibe em megabytes
free -m
~~~

### `top`
**Resumo:** Apresenta uma visualização dinâmica em tempo real dos processos em execução, ordenados por consumo de recursos.
**Exemplos:**
~~~bash
# Inicia o top com atualização padrão
top

# Ordena processos por uso de memória (após iniciar, pressione 'M')
top

# Ordena processos por uso de CPU (após iniciar, pressione 'P')
top

# Filtra apenas processos de um usuário específico
top -u usuario

# Exibe apenas processos com determinado PID
top -p 1234,5678

# Modo batch: executa 5 iterações e salva em arquivo
top -b -n 5 > relatorio.txt
~~~

### `htop`
**Resumo:** Uma alternativa interativa e visualmente mais amigável ao `top`, permitindo a navegação e o gerenciamento de processos com o teclado.
**Exemplos:**
~~~bash
# Inicia o htop com exibição padrão
htop

# Ordena por uso de memória (pressione F6 e selecione PERCENT_MEM)
htop

# Filtra por nome de processo (pressione F4 e digite o nome)
htop

# Exibe apenas processos de um usuário específico
htop -u usuario

# Mostra a árvore de processos (pressione F5)
htop
~~~

### `btop`
**Resumo:** Um monitor de recursos avançado e moderno, com interface gráfica no terminal, exibindo uso de CPU, memória, redes e discos.
**Exemplos:**
~~~bash
# Inicia o btop com interface padrão
btop

# Inicia com tema específico
btop --theme Default

# Exibe apenas informações de CPU
btop --preset cpu

# Inicia em modo minimalista
btop --tty-on
~~~

---

## 2. Identificação e Informações do Sistema

### `uname`
**Resumo:** Imprime informações sobre o sistema operacional e o kernel em uso.
**Exemplos:**
~~~bash
# Exibe todas as informações do sistema
uname -a

# Exibe apenas o nome do kernel
uname -s

# Exibe a versão do kernel
uname -r

# Exibe a arquitetura do hardware
uname -m

# Exibe o nome do nó (hostname)
uname -n

# Exibe a versão do sistema operacional
uname -v
~~~

### `lsb-release`
**Resumo:** Exibe informações de conformidade com o Linux Standard Base (LSB) e detalhes específicos da distribuição.
**Exemplos:**
~~~bash
# Exibe todas as informações LSB disponíveis
lsb_release -a

# Exibe apenas a descrição da distribuição
lsb_release -d

# Exibe apenas o nome da distribuição
lsb_release -i

# Exibe apenas a versão da distribuição
lsb_release -r

# Exibe o codinome da distribuição (ex: focal, jammy)
lsb_release -c
~~~

### `os-release`
**Resumo:** Não é um comando executável, mas um arquivo de configuração que contém dados de identificação do sistema operacional.
**Exemplos:**
~~~bash
# Exibe todo o conteúdo do arquivo os-release
cat /etc/os-release

# Busca apenas o nome da distribuição
grep ^NAME /etc/os-release

# Busca apenas a versão
grep ^VERSION /etc/os-release

# Exibe informações do sistema usando source
source /etc/os-release && echo $PRETTY_NAME
~~~

### `cat`
**Resumo:** Concatena arquivos e imprime seu conteúdo na saída padrão (terminal).
**Exemplos:**
~~~bash
# Exibe o conteúdo de um arquivo
cat arquivo.txt

# Exibe o conteúdo com numeração de linhas
cat -n arquivo.txt

# Exibe múltiplos arquivos em sequência
cat arquivo1.txt arquivo2.txt

# Concatena dois arquivos em um novo
cat arquivo1.txt arquivo2.txt > combinado.txt

# Exibe o conteúdo numerando apenas linhas não vazias
cat -b arquivo.txt

# Exibe caracteres especiais (tabs, quebras de linha)
cat -A arquivo.txt
~~~

### `nano`
**Resumo:** Um editor de texto simples e intuitivo baseado em terminal, ideal para edições rápidas.
**Exemplos:**
~~~bash
# Abre um arquivo para edição
nano arquivo.txt

# Abre um arquivo com numeração de linhas visível
nano -l arquivo.txt

# Abre um arquivo em modo somente leitura
nano -v arquivo.txt

# Abre um arquivo posicionando o cursor na linha 10, coluna 5
nano +10,5 arquivo.txt

# Cria um backup do arquivo original antes de editar
nano -B arquivo.txt

# Abre com busca e substituição automática habilitada
nano -E arquivo.txt
~~~

---

## 3. Navegação e Manipulação de Arquivos e Diretórios

### `pwd`
**Resumo:** Imprime o nome do diretório de trabalho atual (*Print Working Directory*).
**Exemplos:**
~~~bash
# Exibe o diretório atual (caminho lógico)
pwd

# Exibe o diretório atual (caminho físico, resolvendo links simbólicos)
pwd -P

# Armazena o diretório atual em uma variável
DIR_ATUAL=$(pwd)
echo "Você está em: $DIR_ATUAL"
~~~

### `ls`
**Resumo:** Lista o conteúdo de diretórios.
**Exemplos:**
~~~bash
# Lista arquivos do diretório atual
ls

# Lista com detalhes completos (permissões, dono, tamanho, data)
ls -l

# Lista todos os arquivos, incluindo ocultos
ls -la

# Lista em formato legível para humanos (tamanhos em KB, MB, GB)
ls -lh

# Lista ordenado por data de modificação (mais recente primeiro)
ls -lt

# Lista ordenado por tamanho (maior primeiro)
ls -lS

# Lista recursivamente todos os subdiretórios
ls -R

# Lista apenas diretórios
ls -d */

# Lista com cores para diferenciar tipos de arquivo
ls --color=auto
~~~

### `man`
**Resumo:** Exibe o manual de referência de qualquer comando.
**Exemplos:**
~~~bash
# Exibe o manual do comando ls
man ls

# Exibe o manual de uma chamada de sistema (seção 2)
man 2 open

# Exibe o manual de um arquivo de configuração (seção 5)
man 5 passwd

# Busca por uma palavra-chave nos manuais
man -k network

# Exibe apenas a descrição curta de um comando
whatis ls
~~~

### `cd`
**Resumo:** Altera o diretório de trabalho atual (*Change Directory*).
**Exemplos:**
~~~bash
# Vai para o diretório home do usuário
cd

# Vai para o diretório home explicitamente
cd ~

# Vai para o diretório anterior
cd -

# Vai para a raiz do sistema
cd /

# Vai para um diretório específico
cd /var/log

# Vai para o diretório pai (um nível acima)
cd ..

# Vai dois níveis acima
cd ../..
~~~

### `mkdir`
**Resumo:** Cria um novo diretório (pasta).
**Exemplos:**
~~~bash
# Cria um diretório simples
mkdir novo_diretorio

# Cria múltiplos diretórios de uma vez
mkdir dir1 dir2 dir3

# Cria diretórios com permissões específicas (rwxr-xr-x)
mkdir -m 755 diretorio_seguro

# Cria uma estrutura de diretórios aninhados
mkdir -p projetos/python/2026/modulo1

# Cria diretórios com verbose (mostra o que está sendo criado)
mkdir -v novo_diretorio
~~~

### `cp`
**Resumo:** Copia arquivos ou diretórios de uma origem para um destino.
**Exemplos:**
~~~bash
# Copia um arquivo para outro local
cp arquivo.txt /destino/

# Copia e renomeia o arquivo
cp arquivo.txt /destino/novo_nome.txt

# Copia recursivamente um diretório inteiro
cp -r diretorio_origem/ diretorio_destino/

# Copia preservando permissões, dono e timestamps
cp -p arquivo.txt /destino/

# Copia preservando todos os atributos (incluindo links)
cp -a diretorio_origem/ diretorio_destino/

# Copia apenas se o arquivo de origem for mais recente
cp -u arquivo.txt /destino/

# Pede confirmação antes de sobrescrever
cp -i arquivo.txt /destino/

# Força a cópia sem perguntar
cp -f arquivo.txt /destino/

# Copia com barra de progresso (verbose)
cp -v arquivo.txt /destino/
~~~

### `mv`
**Resumo:** Move ou renomeia arquivos e diretórios.
**Exemplos:**
~~~bash
# Renomeia um arquivo
mv arquivo_antigo.txt arquivo_novo.txt

# Move um arquivo para outro diretório
mv arquivo.txt /destino/

# Move múltiplos arquivos para um diretório
mv arquivo1.txt arquivo2.txt /destino/

# Move um diretório inteiro
mv diretorio_origem/ /destino/

# Pede confirmação antes de sobrescrever
mv -i arquivo.txt /destino/

# Força o movimento sem perguntar
mv -f arquivo.txt /destino/

# Move com verbose (mostra o que está sendo feito)
mv -v arquivo.txt /destino/

# Move apenas se o arquivo de origem for mais recente
mv -u arquivo.txt /destino/
~~~

### `rm`
**Resumo:** Remove arquivos ou diretórios permanentemente.
**Exemplos:**
~~~bash
# Remove um arquivo
rm arquivo.txt

# Remove múltiplos arquivos
rm arquivo1.txt arquivo2.txt arquivo3.txt

# Remove um diretório vazio
rm diretorio_vazio

# Remove um diretório e todo seu conteúdo recursivamente
rm -r diretorio/

# Remove forçadamente sem perguntar
rm -f arquivo.txt

# Remove recursivamente e forçadamente (CUIDADO!)
rm -rf diretorio/

# Pede confirmação antes de cada remoção
rm -i arquivo.txt

# Remove com verbose (mostra o que está sendo removido)
rm -v arquivo.txt

# Remove apenas arquivos específicos com padrão
rm *.log
rm -r *.tmp
~~~

---

## 4. Gerenciamento de Pacotes

### `apt`
**Resumo:** Ferramenta de linha de comando para gerenciamento de pacotes em distribuições baseadas em Debian, utilizada para instalar, remover e atualizar softwares.
**Exemplos:**
~~~bash
# Atualiza a lista de pacotes disponíveis
sudo apt update

# Atualiza todos os pacotes instalados
sudo apt upgrade

# Atualiza pacotes e remove dependências obsoletas
sudo apt full-upgrade

# Instala um pacote específico
sudo apt install nome_do_pacote

# Instala múltiplos pacotes
sudo apt install pacote1 pacote2 pacote3

# Remove um pacote (mantém arquivos de configuração)
sudo apt remove nome_do_pacote

# Remove um pacote e seus arquivos de configuração
sudo apt purge nome_do_pacote

# Remove pacotes não mais necessários (dependências órfãs)
sudo apt autoremove

# Busca por um pacote nos repositórios
apt search termo_de_busca

# Exibe informações sobre um pacote
apt show nome_do_pacote

# Lista todos os pacotes instalados
apt list --installed

# Lista pacotes com atualizações disponíveis
apt list --upgradable

# Limpa o cache de pacotes baixados
sudo apt clean

# Remove apenas pacotes .deb obsoletos do cache
sudo apt autoclean

# Baixa o pacote sem instalá-lo
apt download nome_do_pacote

# Verifica dependências de um pacote
apt depends nome_do_pacote
~~~

---

## 5. Controle do Sistema e Gerenciamento de Serviços

### `shutdown`
**Resumo:** Ordena o desligamento, reinicialização ou parada do sistema de forma segura.
**Exemplos:**
~~~bash
# Desliga o sistema imediatamente
sudo shutdown -h now

# Desliga o sistema em 10 minutos
sudo shutdown -h +10

# Desliga o sistema às 22:30
sudo shutdown -h 22:30

# Reinicia o sistema imediatamente
sudo shutdown -r now

# Reinicia o sistema em 5 minutos
sudo shutdown -r +5

# Cancela um agendamento de desligamento
sudo shutdown -c

# Desliga com mensagem para usuários logados
sudo shutdown -h +5 "Sistema será desligado para manutenção"

# Apenas para o sistema (não desliga a energia)
sudo shutdown -H now
~~~

### `systemctl`
**Resumo:** Ferramenta central para inspecionar e controlar o gerenciador de sistema e serviços `systemd`.
**Exemplos:**
~~~bash
# Inicia um serviço
sudo systemctl start nome_servico

# Para um serviço
sudo systemctl stop nome_servico

# Reinicia um serviço
sudo systemctl restart nome_servico

# Recarrega a configuração de um serviço sem reiniciar
sudo systemctl reload nome_servico

# Habilita um serviço para iniciar no boot
sudo systemctl enable nome_servico

# Desabilita um serviço do boot
sudo systemctl disable nome_servico

# Verifica o status de um serviço
systemctl status nome_servico

# Lista todos os serviços ativos
systemctl list-units --type=service

# Lista todos os serviços (ativos e inativos)
systemctl list-units --type=service --all

# Lista serviços que falharam
systemctl --failed

# Exibe os logs de um serviço
journalctl -u nome_servico

# Exibe os logs em tempo real
journalctl -u nome_servico -f

# Mascara um serviço (impede que seja iniciado)
sudo systemctl mask nome_servico

# Desmascara um serviço
sudo systemctl unmask nome_servico

# Verifica se um serviço está ativo
systemctl is-active nome_servico

# Verifica se um serviço está habilitado
systemctl is-enabled nome_servico
~~~

### Runlevels systemd
**Resumo:** No `systemd`, os "runlevels" tradicionais foram substituídos por "targets" (alvos), que representam estados específicos do sistema.
**Exemplos:**
~~~bash
# Exibe o target padrão atual
systemctl get-default

# Lista todos os targets disponíveis
systemctl list-units --type=target

# Altera o target padrão para multi-usuário (equivalente ao runlevel 3)
sudo systemctl set-default multi-user.target

# Altera o target padrão para gráfico (equivalente ao runlevel 5)
sudo systemctl set-default graphical.target

# Muda para o target de resgate (modo de recuperação)
sudo systemctl isolate rescue.target

# Muda para o target de emergência
sudo systemctl isolate emergency.target

# Equivalência entre runlevels e targets:
# Runlevel 0 -> poweroff.target (desligar)
# Runlevel 1 -> rescue.target (modo single-user)
# Runlevel 3 -> multi-user.target (multi-usuário sem GUI)
# Runlevel 5 -> graphical.target (multi-usuário com GUI)
# Runlevel 6 -> reboot.target (reiniciar)
~~~

---

## 6. Rastreamento e Depuração de Processos

### `strace`
**Resumo:** Rastreia as chamadas de sistema (system calls) e os sinais recebidos por um processo.
**Exemplos:**
~~~bash
# Rastreia todas as chamadas de sistema de um comando
strace ls

# Rastreia um processo já em execução
strace -p 1234

# Salva a saída em um arquivo
strace -o saida.txt ls

# Rastreia apenas chamadas de arquivo
strace -e trace=file ls

# Rastreia apenas chamadas de rede
strace -e trace=network ping google.com

# Rastreia com timestamps
strace -T ls

# Rastreia processos filhos (forks)
strace -f ls -R

# Rastreia com contagem de chamadas
strace -c ls

# Rastreia com estatísticas de tempo
strace -c -T ls

# Limita o tamanho das strings exibidas
strace -s 200 ls
~~~

### `ltrace`
**Resumo:** Rastreia as chamadas de bibliotecas dinâmicas (library calls) realizadas por um processo.
**Exemplos:**
~~~bash
# Rastreia todas as chamadas de biblioteca de um comando
ltrace ls

# Rastreia um processo já em execução
ltrace -p 1234

# Salva a saída em um arquivo
ltrace -o saida.txt ls

# Rastreia apenas chamadas específicas
ltrace -e malloc ls

# Rastreia com contagem de chamadas
ltrace -c ls

# Rastreia processos filhos
ltrace -f ls

# Rastreia com timestamps
ltrace -T ls

# Limita a profundidade do rastreamento
ltrace -D 2 ls
~~~

---

## 7. Gerenciamento de Boot e Agendamento

### `grub`
**Resumo:** O GRand Unified Bootloader é o gerenciador de inicialização padrão. O comando `grub-mkconfig` é usado para atualizar suas configurações.
**Exemplos:**
~~~bash
# Atualiza o arquivo de configuração do GRUB
sudo grub-mkconfig -o /boot/grub/grub.cfg

# Atualiza o GRUB em sistemas UEFI
sudo grub-mkconfig -o /boot/efi/EFI/ubuntu/grub.cfg

# Instala o GRUB em um disco específico
sudo grub-install /dev/sda

# Instala o GRUB com opções específicas
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi

# Exibe a versão do GRUB
grub-install --version

# Edita o arquivo de configuração do GRUB
sudo nano /etc/default/grub

# Após editar /etc/default/grub, atualize o GRUB
sudo update-grub

# Adiciona parâmetros ao kernel no GRUB
# Edite GRUB_CMDLINE_LINUX_DEFAULT em /etc/default/grub
# Exemplo: GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"
~~~

### `crontab`
**Resumo:** Permite a criação, edição e visualização de tabelas de agendamento de tarefas automatizadas (cron).
**Exemplos:**
~~~bash
# Edita o crontab do usuário atual
crontab -e

# Lista as tarefas agendadas do usuário atual
crontab -l

# Remove todas as tarefas agendadas
crontab -r

# Edita o crontab de outro usuário (requer root)
sudo crontab -u usuario -e

# Lista as tarefas de outro usuário
sudo crontab -u usuario -l

# Formato do crontab:
# minuto hora dia_do_mês mês dia_da_semana comando
#
# Exemplos práticos:
# Executa todos os dias às 3:00 da manhã
0 3 * * * /caminho/para/script.sh

# Executa a cada 5 minutos
*/5 * * * * /caminho/para/script.sh

# Executa toda segunda-feira às 8:30
30 8 * * 1 /caminho/para/script.sh

# Executa no primeiro dia de cada mês às 00:00
0 0 1 * * /caminho/para/script.sh

# Executa a cada hora
0 * * * * /caminho/para/script.sh

# Executa em dias específicos da semana (seg, qua, sex)
0 9 * * 1,3,5 /caminho/para/script.sh

# Redireciona saída para arquivo de log
0 3 * * * /caminho/para/script.sh >> /var/log/meu_script.log 2>&1
~~~

---

## 8. Monitoramento de Disco, Sessões e Logs

### `df`
**Resumo:** Relata o uso do espaço em disco dos sistemas de arquivos montados (*Disk Free*).
**Exemplos:**
~~~bash
# Exibe o uso de disco em formato legível
df -h

# Exibe em megabytes
df -m

# Exibe em gigabytes
df -G

# Exibe informações de todos os sistemas de arquivos
df -a

# Exibe apenas sistemas de arquivos específicos
df -t ext4

# Exibe excluindo tipos específicos
df -x tmpfs

# Exibe com informações de inodes
df -i

# Exibe o tipo de sistema de arquivos
df -T

# Exibe apenas informações do sistema de arquivos raiz
df -h /

# Exibe uso de disco de um diretório específico
df -h /home
~~~

### `last`
**Resumo:** Exibe uma lista das últimas sessões de login dos usuários, lendo o arquivo `/var/log/wtmp`.
**Exemplos:**
~~~bash
# Exibe todos os logins recentes
last

# Exibe apenas os 10 últimos logins
last -10

# Exibe logins de um usuário específico
last usuario

# Exibe logins de um terminal específico
last tty1

# Exibe com data e hora completas
last -F

# Exibe logins até uma data específica
last -t 20260921120000

# Exibe logins desde uma data específica
last -s 20260901000000

# Exibe em formato legível (IPs em vez de hostnames)
last -i

# Exibe logins de reboots do sistema
last reboot

# Exibe logins de desligamentos
last shutdown
~~~

### `history`
**Resumo:** Exibe o histórico de comandos digitados pelo usuário atual no terminal.
**Exemplos:**
~~~bash
# Exibe todo o histórico de comandos
history

# Exibe os últimos 20 comandos
history 20

# Busca comandos que contenham uma palavra específica
history | grep apt

# Executa o comando número 123 do histórico
!123

# Executa o último comando que começou com "ls"
!ls

# Repete o último comando
!!

# Executa o último comando com sudo
sudo !!

# Limpa o histórico
history -c

# Remove uma entrada específica do histórico
history -d 123

# Salva o histórico atual no arquivo
history -w

# Lê o histórico do arquivo
history -r

# Exibe o histórico com timestamps
HISTTIMEFORMAT="%d/%m/%Y %T " history
~~~

### `dmesg`
**Resumo:** Exibe ou controla o buffer de anel do kernel (*kernel ring buffer*), contendo mensagens de inicialização e eventos de hardware.
**Exemplos:**
~~~bash
# Exibe todas as mensagens do kernel
dmesg

# Exibe as últimas 20 linhas
dmesg | tail -20

# Exibe com timestamps legíveis
dmesg -T

# Exibe apenas mensagens de erro
dmesg --level=err

# Exibe apenas mensagens de aviso
dmesg --level=warn

# Exibe mensagens de um dispositivo específico
dmesg | grep usb

# Exibe mensagens relacionadas a disco
dmesg | grep sda

# Limpa o buffer do kernel
sudo dmesg -C

# Exibe mensagens em tempo real (similar a tail -f)
dmesg -w

# Exibe informações de hardware detectado
dmesg | grep -i memory

# Exibe mensagens de rede
dmesg | grep -i eth
~~~

---

## 9. Data, Hora e Hardware

### `date`
**Resumo:** Exibe ou configura a data e a hora do sistema.
**Exemplos:**
~~~bash
# Exibe a data e hora atual
date

# Exibe em formato específico
date "+%d/%m/%Y %H:%M:%S"

# Exibe apenas a data
date "+%Y-%m-%d"

# Exibe apenas a hora
date "+%H:%M:%S"

# Exibe o dia da semana
date "+%A"

# Exibe o timestamp Unix
date +%s

# Converte timestamp Unix para data legível
date -d @1695312000

# Exibe a data de amanhã
date -d "tomorrow"

# Exibe a data de 7 dias atrás
date -d "7 days ago"

# Configura a data e hora do sistema (requer root)
sudo date -s "2026-09-21 14:30:00"

# Exibe a data em formato RFC 3339
date --rfc-3339=seconds

# Exibe em formato UTC
date -u
~~~

### `hwclock`
**Resumo:** Ferramenta para acesso ao relógio de hardware (RTC), permitindo sincronizá-lo com o relógio do sistema.
**Exemplos:**
~~~bash
# Exibe a hora do relógio de hardware
sudo hwclock --show

# Sincroniza o relógio do sistema com o hardware
sudo hwclock --hctosys

# Sincroniza o relógio de hardware com o sistema
sudo hwclock --systohc

# Define a hora do relógio de hardware
sudo hwclock --set --date="2026-09-21 14:30:00"

# Exibe em UTC
sudo hwclock --show --utc

# Exibe em hora local
sudo hwclock --show --localtime

# Sincroniza com servidor NTP antes
sudo hwclock --systz
~~~

### `fdisk`
**Resumo:** Manipulador de tabelas de partição de disco, utilizado para criar, deletar e modificar partições.
**Exemplos:**
~~~bash
# Lista todas as partições de todos os discos
sudo fdisk -l

# Lista partições de um disco específico
sudo fdisk -l /dev/sda

# Inicia o fdisk interativo para um disco
sudo fdisk /dev/sda

# Dentro do fdisk interativo:
# p - lista as partições
# n - cria nova partição
# d - deleta uma partição
# t - altera o tipo de partição
# w - grava as alterações e sai
# q - sai sem gravar

# Cria uma partição primária
sudo fdisk /dev/sda
# (dentro do fdisk: n -> p -> 1 -> Enter -> Enter -> w)

# Lista partições em formato legível
sudo fdisk -l -h
~~~

### `lspci`
**Resumo:** Lista todos os dispositivos conectados ao barramento PCI.
**Exemplos:**
~~~bash
# Lista todos os dispositivos PCI
lspci

# Lista com informações detalhadas
lspci -v

# Lista com informações muito detalhadas
lspci -vv

# Lista com informações completas (incluindo IRQs e memória)
lspci -vvv

# Lista de forma concisa (uma linha por dispositivo)
lspci -q

# Lista apenas dispositivos de rede
lspci | grep -i net

# Lista apenas placas de vídeo
lspci | grep -i vga

# Lista apenas controladores de áudio
lspci | grep -i audio

# Lista com informações do kernel driver
lspci -k

# Lista em formato numérico (IDs)
lspci -n

# Lista dispositivos de uma classe específica
lspci -d 8086:
~~~

### `lsusb`
**Resumo:** Lista todos os dispositivos conectados aos barramentos USB.
**Exemplos:**
~~~bash
# Lista todos os dispositivos USB
lsusb

# Lista com informações detalhadas
lsusb -v

# Lista com informações muito detalhadas
lsusb -vv

# Lista apenas um dispositivo específico
lsusb -s 001:002

# Lista dispositivos de um hub específico
lsusb -D /dev/bus/usb/001/002

# Lista com IDs numéricos
lsusb -t

# Lista apenas dispositivos de armazenamento
lsusb | grep -i storage

# Lista apenas webcams
lsusb | grep -i camera
~~~

### `disktype`
**Resumo:** Detecta o tipo de conteúdo de um disco, partição ou arquivo de imagem.
**Exemplos:**
~~~bash
# Detecta o tipo de conteúdo de um disco
disktype /dev/sda

# Detecta o tipo de uma partição específica
disktype /dev/sda1

# Detecta o tipo de um arquivo de imagem
disktype imagem.iso

# Detecta com informações detalhadas
disktype -v /dev/sda

# Detecta apenas o tipo de sistema de arquivos
disktype /dev/sda1 | grep "file system"
~~~

### `lshw`
**Resumo:** Extrai informações detalhadas sobre a configuração de hardware do sistema.
**Exemplos:**
~~~bash
# Exibe informações completas de hardware
sudo lshw

# Exibe em formato curto (resumido)
sudo lshw -short

# Exibe informações de hardware específico
sudo lshw -C memory

# Exibe informações de CPU
sudo lshw -C processor

# Exibe informações de disco
sudo lshw -C disk

# Exibe informações de rede
sudo lshw -C network

# Exibe em formato HTML
sudo lshw -html > hardware.html

# Exibe em formato JSON
sudo lshw -json

# Exibe em formato XML
sudo lshw -xml

# Exibe apenas informações de barramento
sudo lshw -C bus
~~~

### `hwinfo`
**Resumo:** Ferramenta abrangente de sondagem de hardware, fornecendo detalhes extensos sobre os componentes do sistema.
**Exemplos:**
~~~bash
# Exibe informações completas de hardware
hwinfo

# Exibe em formato curto
hwinfo --short

# Exibe informações de hardware específico
hwinfo --cpu

# Exibe informações de memória
hwinfo --memory

# Exibe informações de disco
hwinfo --disk

# Exibe informações de rede
hwinfo --network

# Exibe informações de USB
hwinfo --usb

# Exibe informações de PCI
hwinfo --pci

# Exibe informações de monitor
hwinfo --monitor

# Exibe informações de BIOS
hwinfo --bios

# Salva em arquivo
hwinfo > hardware_info.txt
~~~

---

## 10. O Sistema de Arquivos Virtual

### `/proc`
**Resumo:** Não é um comando, mas um sistema de arquivos virtual que fornece uma interface para as estruturas de dados do kernel e informações dos processos.
**Exemplos:**
~~~bash
# Exibe informações da CPU
cat /proc/cpuinfo

# Exibe informações de memória
cat /proc/meminfo

# Exibe informações do kernel
cat /proc/version

# Exibe informações de uptime
cat /proc/uptime

# Exibe informações de carga do sistema
cat /proc/loadavg

# Exibe informações de um processo específico (PID 1234)
cat /proc/1234/status
cat /proc/1234/cmdline
cat /proc/1234/environ

# Lista todos os processos
ls /proc | grep -E '^[0-9]+$'

# Exibe informações de filesystems
cat /proc/filesystems

# Exibe informações de particionamento
cat /proc/partitions

# Exibe informações de mounts
cat /proc/mounts

# Exibe informações de rede
cat /proc/net/dev

# Exibe informações de interrupt
cat /proc/interrupts

# Exibe informações de DMA
cat /proc/dma

# Exibe informações de I/O
cat /proc/diskstats
~~~

---

## 11. Gerenciamento de Módulos do Kernel

### `lsmod`
**Resumo:** Exibe a lista de módulos do kernel que estão atualmente carregados na memória.
**Exemplos:**
~~~bash
# Lista todos os módulos carregados
lsmod

# Lista com formatação mais legível
lsmod | column -t

# Busca um módulo específico
lsmod | grep usb

# Lista módulos de rede
lsmod | grep -i net

# Lista módulos de áudio
lsmod | grep snd

# Lista módulos de vídeo
lsmod | grep drm

# Conta quantos módulos estão carregados
lsmod | wc -l

# Lista módulos ordenados por tamanho
lsmod | sort -k2 -n -r
~~~

### `pcimodules`
**Resumo:** *Nota: Este comando foi descontinuado e removido em kernels Linux modernos.* Anteriormente, listava módulos PCI compatíveis.
**Exemplos (Alternativas modernas):**
~~~bash
# Lista módulos associados a dispositivos PCI
lspci -k

# Lista informações detalhadas de um dispositivo PCI
lspci -v -s 00:1f.0

# Busca módulos disponíveis para um dispositivo
modinfo $(lspci -n -s 00:1f.0 | awk '{print $3}' | cut -d: -f1)

# Lista todos os módulos disponíveis
find /lib/modules/$(uname -r) -name "*.ko"

# Lista módulos com informações
modinfo nome_do_modulo
~~~

### `insmod`
**Resumo:** Insere (carrega) um módulo do kernel manualmente a partir de um arquivo `.ko` específico.
**Exemplos:**
~~~bash
# Carrega um módulo a partir de um arquivo
sudo insmod /caminho/para/modulo.ko

# Carrega um módulo com parâmetros
sudo insmod modulo.ko parametro1=valor1 parametro2=valor2

# Carrega um módulo e exibe mensagens
sudo insmod -v modulo.ko

# Carrega um módulo com syslog
sudo insmod -s modulo.ko

# Verifica se o módulo foi carregado
lsmod | grep modulo
~~~

### `rmmod`
**Resumo:** Remove (descarrega) um módulo do kernel da memória, desde que não esteja em uso.
**Exemplos:**
~~~bash
# Remove um módulo
sudo rmmod nome_do_modulo

# Remove múltiplos módulos
sudo rmmod modulo1 modulo2

# Remove com verbose
sudo rmmod -v nome_do_modulo

# Remove forçadamente (se possível)
sudo rmmod -f nome_do_modulo

# Remove e exibe mensagens no syslog
sudo rmmod -s nome_do_modulo

# Verifica se o módulo foi removido
lsmod | grep modulo
~~~

### `modprobe`
**Resumo:** Adiciona ou remove módulos do kernel de forma inteligente, resolvendo automaticamente as dependências entre eles.
**Exemplos:**
~~~bash
# Carrega um módulo (com dependências)
sudo modprobe nome_do_modulo

# Carrega um módulo com parâmetros
sudo modprobe nome_do_modulo parametro=valor

# Remove um módulo (com dependências)
sudo modprobe -r nome_do_modulo

# Carrega um módulo com verbose
sudo modprobe -v nome_do_modulo

# Exibe as dependências de um módulo
modprobe --show-depends nome_do_modulo

# Lista todos os módulos disponíveis
modprobe -l

# Carrega um módulo em modo dry-run (não carrega de verdade)
sudo modprobe -n nome_do_modulo

# Recarrega a configuração de módulos
sudo modprobe -c
~~~

### `depmod`
**Resumo:** Gera o arquivo `modules.dep` e os mapas de dependências, informando ao sistema quais módulos dependem de outros.
**Exemplos:**
~~~bash
# Gera dependências para o kernel atual
sudo depmod -a

# Gera dependências para um kernel específico
sudo depmod -a 5.15.0-76-generic

# Gera com verbose
sudo depmod -av

# Gera apenas para módulos específicos
sudo depmod modulo1 modulo2

# Exibe as dependências de um módulo
depmod -e nome_do_modulo

# Gera em modo dry-run
sudo depmod -n
~~~

---

## 12. Atualização de Kernel

### Atualização de Kernel
**Resumo:** O processo de atualização do kernel Linux é geralmente realizado via gerenciador de pacotes da distribuição.
**Exemplos:**
~~~bash
# Debian/Ubuntu - Atualiza o kernel para a versão mais recente
sudo apt update
sudo apt install --only-upgrade linux-image-generic
sudo apt install --only-upgrade linux-headers-generic

# Debian/Ubuntu - Instala uma versão específica do kernel
sudo apt install linux-image-5.15.0-76-generic

# Debian/Ubuntu - Lista kernels disponíveis
apt search linux-image

# Debian/Ubuntu - Lista kernels instalados
dpkg --list | grep linux-image

# Debian/Ubuntu - Remove um kernel antigo
sudo apt remove linux-image-5.4.0-42-generic

# Debian/Ubuntu - Remove kernels não utilizados
sudo apt autoremove

# Fedora/RHEL - Atualiza o kernel
sudo dnf update kernel

# Fedora/RHEL - Lista kernels instalados
rpm -qa kernel

# Fedora/RHEL - Remove kernel antigo
sudo dnf remove kernel-5.4.0

# Arch Linux - Atualiza o kernel
sudo pacman -Syu linux

# Arch Linux - Instala kernel LTS
sudo pacman -S linux-lts

# Verifica a versão atual do kernel
uname -r

# Lista todos os kernels instalados no sistema
ls /boot/vmlinuz-*

# Atualiza o GRUB após instalação de kernel
sudo update-grub

# Gera o initramfs manualmente
sudo update-initramfs -u
~~~

---

## 13. Gerenciamento de Usuários e Grupos

### `su`
**Resumo:** Permite que um usuário assuma a identidade de outro usuário (Substitute User).
**Exemplos:**
~~~bash
# Assume o usuário root (mantém ambiente atual)
su

# Assume o usuário root com ambiente limpo
su -

# Assume outro usuário específico
su usuario

# Assume outro usuário com ambiente limpo
su - usuario

# Executa um comando como outro usuário
su - usuario -c "comando"

# Executa um comando como root
su -c "comando"

# Assume usuário sem pedir senha (se configurado)
su - usuario

# Executa shell específico como outro usuário
su -s /bin/bash usuario
~~~

### Usuários e Grupos
**Resumo:** O gerenciamento de usuários e grupos é realizado através de comandos dedicados.
**Exemplos:**
~~~bash
# === CRIAÇÃO DE USUÁRIOS ===

# Cria um usuário simples
sudo useradd novo_usuario

# Cria um usuário com diretório home
sudo useradd -m novo_usuario

# Cria um usuário com shell específico
sudo useradd -s /bin/bash novo_usuario

# Cria um usuário com grupo primário específico
sudo useradd -g grupo_principal novo_usuario

# Cria um usuário com grupos secundários
sudo useradd -G grupo1,grupo2 novo_usuario

# Cria um usuário com data de expiração
sudo useradd -e 2026-12-31 novo_usuario

# Cria um usuário com comentário (GECOS)
sudo useradd -c "Nome Completo" novo_usuario

# === MODIFICAÇÃO DE USUÁRIOS ===

# Altera o shell de um usuário
sudo usermod -s /bin/zsh usuario

# Adiciona usuário a um grupo secundário
sudo usermod -aG sudo usuario

# Altera o diretório home
sudo usermod -d /novo/home usuario

# Bloqueia uma conta
sudo usermod -L usuario

# Desbloqueia uma conta
sudo usermod -U usuario

# Define data de expiração
sudo usermod -e 2026-12-31 usuario

# === SENHAS ===

# Altera a senha de um usuário
sudo passwd usuario

# Altera a senha do usuário atual
passwd

# Bloqueia a senha de um usuário
sudo passwd -l usuario

# Desbloqueia a senha de um usuário
sudo passwd -u usuario

# Expira a senha imediatamente
sudo passwd -e usuario

# === EXCLUSÃO DE USUÁRIOS ===

# Remove um usuário (mantém arquivos)
sudo userdel usuario

# Remove um usuário e seu diretório home
sudo userdel -r usuario

# === CRIAÇÃO DE GRUPOS ===

# Cria um grupo
sudo groupadd novo_grupo

# Cria um grupo com GID específico
sudo groupadd -g 1500 novo_grupo

# Cria um grupo de sistema
sudo groupadd -r grupo_sistema

# === MODIFICAÇÃO DE GRUPOS ===

# Altera o nome de um grupo
sudo groupmod -n novo_nome nome_antigo

# Altera o GID de um grupo
sudo groupmod -g 2000 grupo

# === EXCLUSÃO DE GRUPOS ===

# Remove um grupo
sudo groupdel grupo

# === INFORMAÇÕES DE USUÁRIOS ===

# Exibe informações de um usuário
id usuario

# Exibe o nome de login
whoami

# Exibe o usuário atual
id -u

# Exibe o grupo atual
id -g

# Lista todos os grupos de um usuário
groups usuario

# Exibe informações detalhadas do usuário
finger usuario

# Lista todos os usuários do sistema
cat /etc/passwd

# Lista usuários com UID >= 1000 (usuários normais)
awk -F: '$3 >= 1000 && $1 != "nobody" {print $1}' /etc/passwd

# === INFORMAÇÕES DE GRUPOS ===

# Lista todos os grupos
cat /etc/group

# Exibe membros de um grupo
getent group grupo

# Lista grupos com GID >= 1000
awk -F: '$3 >= 1000 {print $1}' /etc/group
~~~

---

## Notas Importantes

1. **Privilégios:** Muitos comandos requerem privilégios de superusuário (root). Utilize `sudo` antes do comando ou alterne para o usuário root com `su -`.

2. **Documentação:** Para informações detalhadas sobre qualquer comando, utilize o manual integrado:
   ~~~bash
   man nome_do_comando
   man -k palavra_chave
   info nome_do_comando
   ~~~

3. **Compatibilidade:** Este manual foi elaborado com base em distribuições Linux modernas (2026). Alguns comandos podem variar entre diferentes distribuições.

4. **Segurança:** Sempre verifique a sintaxe dos comandos antes de executá-los, especialmente aqueles que modificam ou removem arquivos e configurações do sistema.

5. **Aliases úteis:**
   ~~~bash
   # Adicione ao ~/.bashrc ou ~/.zshrc
   alias ll='ls -alF'
   alias la='ls -A'
   alias l='ls -CF'
   alias ..='cd ..'
   alias ...='cd ../..'
   alias grep='grep --color=auto'
   ~~~

6. **Redirecionamentos:**
   ~~~bash
   # Redireciona saída padrão
   comando > arquivo.txt

   # Redireciona saída de erro
   comando 2> erro.log

   # Redireciona ambos
   comando > saida.log 2>&1

   # Redireciona entrada
   comando < arquivo.txt

   # Pipeline (conecta saída de um comando à entrada de outro)
   comando1 | comando2
   ~~~

---

## Conclusão

Este manual fornece uma base sólida e abrangente para a administração e operação de sistemas Linux. Os comandos apresentados cobrem desde tarefas básicas de navegação e manipulação de arquivos até operações avançadas de gerenciamento de kernel e serviços do sistema.

Para aprofundamento adicional, recomenda-se:
- Consulta à documentação oficial da distribuição utilizada
- Prática regular dos comandos em ambientes controlados
- Estudo dos manuais completos (`man`) de cada comando
- Participação em comunidades Linux para troca de experiências
- Experimentação em máquinas virtuais ou containers

---

**Fim do Manual**