A arquitetura deste Home-Lab baseia-se no reaproveitamento de hardware legado, otimizando a distribuição de carga de acordo com a capacidade computacional de cada nó.

## 💻 Inventário e Funções
O cluster é composto por duas unidades principais operando em modo "headless" (sem monitor/periféricos próprios):

1. **Nó de Armazenamento e Gestão (Samsung - "O Cérebro"):**
   - **Estado:** Teclado com falhas, operando via rede.
   - **Função:** Atua como o servidor NAS principal, gerenciando o armazenamento de dados, o Docker Engine inicial e serviços de rede leves.

2. **Nó de Processamento Pesado (Lenovo - "O Músculo"):**
   - **Estado:** Botão Power inativo, carcaça danificada.
   - **Capacidade:** Superior para tarefas de IA e Transcodificação de vídeo.
   - **Função:** Destinado a rodar instâncias de IA (LLMs locais), o **Agente Zero** e conversão de streamings. 
   - **Integração:** Após o desenvolvimento no Lenovo, os agentes e modelos otimizados são implantados no servidor para produção.

---

## 🛠️ Recuperação Crítica do Arch Linux (Nó Lenovo)

Para integrar o Lenovo ao cluster, foi necessário realizar uma intervenção de baixo nível devido à corrupção de bibliotecas essenciais que impediam o boot e a atualização do sistema (`libgcc_s.so.1`).

### Procedimento de Concerto (Disaster Recovery)

1. **Identificação da Falha:** Quebra de pacotes base durante atualização via `pacman`, resultando em "Assertion failed" e Kernel Panic.
	1. **Ambiente de Resgate:** Uso do **Athena OS** via SSD externo para realizar o `chroot` no disco interno.
2. **Reparo das Bibliotecas:**
   - Montagem das partições do Arch (`/` e `/boot`).
   - Forçar a reinstalação dos pacotes `gcc-libs` e `glibc` utilizando o cache local do pacman ou repositório remoto via `--overwrite`.
   
      pacman --root /mnt --cachedir /mnt/var/cache/pacman/pkg -S core/gcc-libs --overwrite "*"

4. **Resultado:** Restauração da estabilidade do sistema, permitindo que o nó Lenovo retorne à rede como o processador principal de IA do laboratório.
---

## 🚀 Visão de Futuro (Modularidade)

Ambas as máquinas passarão por modificações físicas:

- Remoção de telas desnecessárias para economia de energia.
    
- Instalação de **SSDs extras** em ambos para expansão de armazenamento e cache.
    
- Acesso remoto total via terminal e interface web, eliminando a dependência de periféricos físicos integrados. 


