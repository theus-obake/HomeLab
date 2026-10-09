# 01 - Instalação do Ubuntu Server

## Objetivo
Transformar um PC antigo em servidor para estudar Linux, redes e segurança.

## Ambiente
- CPU de 2,80 GHz (i7 série 800), 8 GB de RAM DDR3 (1333 MHz), SSD de 240 GB
- Placa-mãe H55 com BIOS AMI (legada, sem UEFI)
- Adaptador Wi-Fi USB TP-Link TL-WN823N (a placa cabeada existe, mas ficou sem cabo)
- Sistema anterior: Linux Mint, substituído nesta instalação

## 1. Preparação do pendrive de boot
1. Baixei a ISO do **Ubuntu Server** (versão Server, não Desktop) no site oficial.
2. Usei o **Rufus** para gravar a ISO em um pendrive simples.
3. Como a máquina é antiga, configurei o Rufus com esquema de partição **MBR** e sistema de destino **BIOS (ou UEFI-CSM)**.

## 2. Boot pelo pendrive
Com o pendrive conectado, liguei o PC e apertei `F11` (menu de boot, "BBS Popup") para escolher o pendrive.

## 3. Instalação
1. **Idioma:** português.
2. **Tipo de instalação:** Ubuntu Server (padrão), sem a versão minimizada e sem busca por drivers de terceiros.
3. **Rede:** o instalador listou duas interfaces, a cabeada (sem cabo) e o adaptador Wi-Fi USB. Usei o Wi-Fi:
   - Selecionei a interface WLAN, depois **Edit Wi-Fi**.
   - Escolhi a rede, digitei a senha e confirmei com Enter.
   - Poucos minutos depois, o instalador mostrou um IPv4 obtido por **DHCPv4**.
4. **Armazenamento:** escolhi **"Use an entire disk"** no SSD de 240 GB, com **LVM** e sem criptografia (LUKS). O instalador criou:
   - Partição 1: BIOS grub spacer (1 MB), o que confirma o boot em BIOS legada
   - Partição 2: `/boot`, ext4, 2 GB
   - Partição 3: volume físico do grupo `ubuntu-vg` (~221 GB)
   - Volume lógico de 100 GB montado em `/`
   - ~121 GB livres no grupo, disponíveis para ampliar depois
5. **Perfil:** defini o nome do servidor (hostname), o usuário administrador e a senha.
6. **SSH:** [ESCREVA AQUI: "marquei Install OpenSSH server no instalador" ou "instalei o openssh-server depois, com apt"]. Login por senha habilitado, sem chave importada.
7. **Finalização:** aguardei a instalação, reiniciei, retirei o pendrive e o servidor iniciou pelo SSD.

## Problemas encontrados

### Não conseguia entrar na BIOS
- **Sintoma:** a tecla da BIOS não era reconhecida no boot.
- **Solução:** resetei a CMOS removendo a pilha CR2032 da placa-mãe por cerca de 5 minutos. Depois do reset, a tela exibiu `Press F1 to Run SETUP` e `Press F11 for BBS POPUP`.

### Erro "BIOS/Legacy boot of UEFI-only media"
- **Causa:** o pendrive tinha sido gravado no Rufus para UEFI, mas a placa só suporta BIOS legada.
- **Solução:** regravei o pendrive com **MBR + BIOS**.

## Resultado
- Ubuntu Server instalado no SSD, conectado à rede por Wi-Fi
- Acesso remoto por SSH a partir do notebook
- ~121 GB do LVM ainda livres

## O que aprendi
- Diferença entre BIOS legada e UEFI, e por que o esquema de partição importa
- Para que serve o reset da CMOS
- Diferença entre o Setup da BIOS (`F1`) e o menu de boot (`F11`)
- Como o LVM separa volumes físicos, grupo e volumes lógicos

## Próximos passos
- Acesso por SSH e firewall (`02-ssh.md`, `03-firewall.md`)
- Reservar o IP do servidor no roteador
- Ampliar o volume lógico com o espaço livre do LVM
