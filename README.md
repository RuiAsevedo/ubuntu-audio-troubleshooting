# Troubleshooting de Áudio e Manutenção de Repositórios - Ubuntu

Este repositório documenta a resolução de problemas de redirecionamento de áudio Bluetooth e correção de erros de repositórios APT encontrados durante o uso do Ubuntu 22.04 LTS em um notebook Dell Inspiron 15 3530.

## 1. Problema de Áudio (Bluetooth vs. Alto-falantes)

**Cenário:** Mesmo com o fone **QCY ArcBuds** conectado e pareado, o áudio de aplicativos como o Google Chrome e Spotify continuava saindo pelos alto-falantes internos do notebook.

### Solução via Terminal (CLI)
Para forçar o redirecionamento imediato, utilizamos o utilitário `pactl`:

1. Identificar o ID do dispositivo de saída (Sink):
   ```bash
   pactl list short sinks

2. Mover o fluxo de áudio do aplicativo para o fone (ID 2):
   pactl move-sink-input [ID_DO_APP] 2

3. Solução Permanente (GUI)
  Instalei o "Pavucontrol" para gerenciar os fluxos de forma granular e persistente:
  Instalação: sudo apt install pavucontrol -y
  Ação: Na aba "Reprodução", vinculei o Google Chrome permanentemente ao dispositivo QCY ArcBuds.

4. Manutenção do Gerenciador de Pacotes (APT)
Cenário: O comando sudo apt update apresentava erros de chave GPG (NO_PUBKEY) devido a um repositório do Spotify corrompido ou antigo.

  Solução
  Removemos a lista de fontes problemática para limpar o processo de atualização:
  
  Bash
  
  sudo rm /etc/apt/sources.list.d/spotify.list
  sudo apt update
  
Tecnologias Utilizadas
  Sistema Operacional: Ubuntu 22.04 LTS
  Hardware: Dell Inspiron 15 3530 / Intel Core i3 100U
  Servidor de Áudio: PulseAudio / PipeWire
