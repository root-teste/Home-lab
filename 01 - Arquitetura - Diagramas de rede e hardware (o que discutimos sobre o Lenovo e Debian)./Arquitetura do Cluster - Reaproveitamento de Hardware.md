# Cluster Híbrido: Estratégia de Hardware Legado

O projeto foca em extrair performance máxima de hardware com danos físicos, mas funcionalidade lógica preservada.

## Dispositivos e Funções:
- **Samsung (Nó 1 - Debian):** Servidor NAS e Gestão de Dados. Responsável pelo armazenamento e serviços 24/7.
- **Lenovo (Nó 2 - Arch/IA):** "O Músculo". Responsável pelo processamento pesado, transcodificação de vídeo e execução do **Agente Zero**.

## Modificações Físicas (Headless):
- Remoção de telas (LCD) para redução de consumo e espaço.
- Operação via SSH/WebUI exclusiva.
- Expansão via SSD extra para otimização de cache de IA.