	**Objetivo:** Transformar um notebook Samsung (tela danificada) em um servidor doméstico 24/7, garantindo que ele não entre em suspensão e permaneça ativo mesmo com a tampa fechada.

---

## 1. Desativação da Suspensão e Hibernação

Para garantir que o sistema nunca entre em estado de baixo consumo ou "durma", os alvos (targets) de suspensão do `systemd` foram mascarados.

- **Comando executado:**
    
    Bash
    
    ```
    sudo systemctl mask sleep.target suspend.target hibernation.target hybrid-sleep.target
    ```
    

## 2. Gerenciamento da Tampa do Notebook (Lid Switch)

Configuração necessária para permitir que o servidor opere com a tampa fechada sem suspender o sistema.

- **Arquivo editado:** `/etc/systemd/logind.conf`
    
- **Modificações:**
    
    - `HandleLidSwitch=ignore`
        
    - `HandleLidSwitchExternalPower=ignore`
        
    - `HandleLidSwitchDocked=ignore`
        
- **Aplicação:** O serviço foi reiniciado com `sudo systemctl restart systemd-logind`.
    

## 3. Gerenciamento de Energia da Tela (DPMS)

Desativação do desligamento automático da tela (screen blanking) via terminal para evitar bugs de energia em hardware antigo.

- **Comando executado:**
    
    Bash
    
    ```
    sudo setterm -blank 0 -powersave off
    ```
    

## 4. Monitoramento e Diagnóstico

Instalação de ferramentas para acompanhamento de recursos (CPU, RAM e Uptime).

- **Ferramenta:** `htop`
    
- **Instalação:**
    
    Bash
    
    ```
    sudo apt update && sudo apt install htop -y
    ```
    

---

## 🚀 Status Atual e Próximos Passos

O hardware agora está **estabilizado para operação contínua**. A máquina não desliga ao fechar a tampa e todos os gatilhos de suspensão foram desativados.

**Próximos Marcos:**

1. **[[01. Instalação do Docker]]:** Base para os serviços (Immich, Nextcloud, Agent-Zero).
    
2. **[[02. Desativar a interface GNOME]]:** Remoção da interface gráfica (GNOME) para otimização de RAM.
    
3. **Segurança:** Configuração de Firewall (UFW) e chaves SSH.
    

---

_Documentação gerada em: 16 de abril de 2026._