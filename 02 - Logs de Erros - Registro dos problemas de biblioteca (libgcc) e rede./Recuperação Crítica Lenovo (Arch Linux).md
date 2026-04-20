## Problema Identificado
O sistema apresentou falha total de boot e impossibilidade de execução de binários básicos devido à corrupção da biblioteca `libgcc_s.so.1`. O erro manifestava-se como:
`Assertion failed: ... libgcc_s.so.1`

## Estratégia de Resgate
Utilizou-se o **Athena OS** (Live/SSD Externo) para intervir no sistema de arquivos do disco interno.

### Passo a Passo da Solução:
1. **Montagem do Sistema:**
   
>	mount /dev/sda2 /mnt
>	mount /dev/sda1 /mnt/boot

2. **Ambiente Chroot:** Tentativa de `arch-chroot`, inicialmente limitada pela quebra de bibliotecas.

3. **Reparo via Pacman Externo:** Comando utilizado para forçar a sobrescrita das bibliotecas corrompidas sem depender do binário quebrado do sistema interno:

>	pacman --root /mnt --cachedir /mnt/var/cache/pacman/pkg -S core/gcc-libs core/glibc --overwrite " * "

   
4. **Verificação:** ~~Após a sobrescrita, o sistema recuperou a capacidade de executar o `pacman` e o `immich-go`, permitindo a conclusão do backup de 47GB.~~

#refazer Não conseguimos rodar os comandos necessários pois hávia mais bibliotecas quebradas o que por si só nos esta impedindo de rodar o comando pacman, mas fez nosso arch-chroot funcionasse e nos possibilitou fazer subir os arquivo, então montamos a partição em nosso ssd externo (Athena) e extraimos os arquivos do GOOGLE FOTOS em nosso SSD, dessa forma conseguimos ultilizar o comando Cli do immich diretamente de nosso AthenaOS apartir do SSD (Adicionar passo a passo da sincronização Do CLI em uma nova aba)

, porem ainda sem as bibliotecas principais seria impossível inicializar o arch normalmente por isso prosseguimos com o concerto do mesmo, após muitas tentativas falhas em atualizar a bibloteca atrávez do pacman do arch resolvemos fazer o processo manualmente pois os dados pareciam não estar sendo alocados no local certo


```
    # Baixando gcc-libs (que contém as duas libs que faltam)
    pacman -Sw core/gcc-libs --cachedir . --dbpath /tmp
    
    