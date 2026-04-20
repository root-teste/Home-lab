# Home-Lab: Private Cloud & Media NAS 🚀

Este projeto documenta a implementação de um ecossistema de servidor doméstico focado em soberania de dados, privacidade e alta performance, substituindo gradualmente serviços de nuvem pública por uma infraestrutura local robusta.

## 🎯 Escopo do Projeto

O sistema foi projetado para centralizar e gerir:

- **Mídia:** Fotos, Vídeos (alta qualidade), Músicas e Filmes (Transcoding via Nó Lenovo).
    
- **Documentos:** PDFs, Notas estruturadas (Obsidian) e arquivos gerais.
    
- **Rede:** Acesso remoto seguro via VPN/Túnel.
    

---

## 🏗️ Arquitetura do Sistema (Cluster Híbrido Headless)

O ecossistema utiliza uma estratégia de **distribuição de carga**, reaproveitando hardware legado para funções específicas. Ambos os nós operam em modo _headless_ (sem telas/periféricos), otimizando espaço e consumo.

### 1. Nó de Armazenamento e Gestão (Samsung - Host Principal)

- **SO:** Debian 13 (Trixie/Testing) - Infraestrutura cabeada (IP `.90`).
    
- **Stack:** Docker Engine + Docker Compose.
    
- **Serviços Ativos:**
    
    - **Immich:** Gestão central de fotos/vídeos com IA.
        
    - **PostgreSQL 16:** Banco de dados relacional para metadados e persistência.
        
    - **Redis:** Cache e gerenciamento de filas de tarefas.
        
    - **Netdata:** Monitoramento de telemetria e saúde do hardware em tempo real.
        

### 2. Nó de Processamento e IA (Lenovo - "O Músculo")

- **SO:** Arch Linux (Recuperado).
    
- **Função:** Destinado a tarefas de alto custo computacional, como execução do **Agente Zero**, modelos de LLM locais e transcodificação de streaming de vídeo.
    
- **Hardware:** Equipado com SSD extra para cache de processamento e swap de IA.
    

---

## 🛠️ Case Study: Recuperação de Desastre (Disaster Recovery)

Durante a fase crítica de migração, o sistema cliente (Arch Linux) sofreu uma corrupção de bibliotecas fundamentais após uma atualização de pacotes interrompida, afetando a `libgcc_s.so.1` e a `libstdc++.so.6`.

**Desafio:** O sistema ficou incapacitado de rodar o `pacman` e o binário `immich-go`.

**Solução Aplicada:**

1. **Ambiente de Resgate:** Uso do **Athena OS** via Live-SSD para intervenção externa.
    
2. **Injeção Manual de Binários:** Como o `pacman --root` falhou devido à quebra da ABI, foi realizada a extração manual dos pacotes `gcc-libs` e `libstdc++` diretamente no ponto de montagem do sistema corrompido (`/mnt`).
    
3. **Restauração:** Reconstrução dos links simbólicos via `ldconfig -r` de fora para dentro, permitindo o retorno do sistema ao estado operacional sem perda de dados.
    

---

## 🔄 Migração de Dados (Google Takeout)

A transição da nuvem pública para o NAS focou na preservação total da integridade dos arquivos.

- **Ferramenta:** `immich-go` (CLI)
    
- **Método:** Importação direta via **Google Takeout**, garantindo que metadados (datas, geolocalização e álbuns) fossem preservados através dos arquivos JSON.
    
- **Volume Processado:** ~47GB de mídia recuperada e indexada com sucesso.
    

---

## 🚀 Próximos Passos (Roadmap)

- [ ] **Backup Automatizado:** Script de dump do Postgres para armazenamento externo frio.
    
- [ ] **Acesso Externo:** Implementação de túnel seguro (Tailscale/Cloudflare) para dispensar abertura de portas no roteador.
    
- [ ] **Obsidian Wiki:** Sincronização automática deste repositório com o GitHub Pages para documentação pública.
    
- [ ] **Modificação Física:** Remoção física dos componentes de LCD dos notebooks para integração definitiva ao rack de servidores.