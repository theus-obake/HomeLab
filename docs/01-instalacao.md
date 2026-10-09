# 01 - Instalação do Ubuntu Server

## Objetivo
Transformar um PC antigo em servidor para estudar Linux, redes e segurança.

## Hardware
- CPU de 2,80 GHz (i7 série 800), 8 GB de RAM DDR3, SSD de 240 GB
- Placa-mãe H55 com BIOS AMI (legada, sem UEFI)
- Adaptador Wi-Fi para conexão com a rede

## 1. Preparação do pendrive de boot
1. Baixei a ISO do Ubuntu Server (versão **Server**, não Desktop) no site oficial.
2. Enquanto a ISO baixava, preparei um pendrive simples para o boot.
3. Usei o **Rufus** para gravar a ISO no pendrive.
4. Como a máquina é antiga, configurei o Rufus com:
   - Esquema de partição: **MBR**
   - Sistema de destino: **BIOS (ou UEFI-CSM)**

## 2. Boot pelo pendrive
Com o pendrive conectado, liguei o PC e apertei `F11` (menu de boot, "BBS Popup") para escolher o pendrive.

## 3. Instalação
1. Mantive a configuração padrão (default).
2. **Rede:** na tela de configuração de rede, usei a interface **WLAN**, porque o servidor se conecta por adaptador Wi-Fi.
   - Selecionei a WLAN não conectada, depois **Edit Wi-Fi**.
   - Escolhi a rede, digitei a senha e confirmei com Enter.
   - Poucos minutos depois, o instalador exibiu um endereço IPv4 obtido por **DHCPv4**.
3. **Armazenamento:** escolhi **"Use an entire disk"**, substituindo o Linux Mint que estava no SSD pelo Ubuntu Server. Usei LVM.
4. Defini o nome do servidor (hostname) e o usuário administrador.

## Problemas encontrados

### Não conseguia entrar na BIOS
- **Sintoma:** a tecla da BIOS não era reconhecida no boot.
- **Solução:** resetei a CMOS removendo a pilha CR2032 da placa-mãe por cerca de 5 minutos. Depois do reset, a tela exibiu `Press F1 to Run SETUP` e `Press F11 for BBS POPUP`.

### Erro "BIOS/Legacy boot of UEFI-only media"
- **Causa:** o pendrive tinha sido gravado no Rufus para UEFI, mas a placa só suporta BIOS legada.
- **Solução:** regravei o pendrive com **MBR + BIOS**.

## O que aprendi
- Diferença entre BIOS legada e UEFI, e por que o esquema de partição importa
- Para que serve o reset da CMOS
- Diferença entre o Setup da BIOS (`F1`) e o menu de boot (`F11`)

## Próximo passo
Acessar o servidor por SSH a partir do notebook (`02-ssh.md`).
