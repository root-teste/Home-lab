### 🛠️ A Extração Manual

Faremos o seguinte: vamos baixar os pacotes manualmente no Athena e "descompactar" o conteúdo deles diretamente dentro do Arch.


1. **Limpar e preparar:**
    
    Bash
    
    ```
    cd /tmp
    mkdir rescue_libs
    cd rescue_libs
    ```
    
2. **Baixar os pacotes (baixaremos direto do repositório oficial do Arch):**
    
    Bash
    
    ```
    # Baixando gcc-libs (que contém as duas libs que faltam)
    pacman -Sw core/gcc-libs --cachedir . --dbpath /tmp
    ```
    
	tar --zstd -xf libgcc-15*.pkg.tar.zst -C /mnt

	tar --zstd -xf libstdc++-15*.pkg.tar.zst -C /mnt

	ls -l /mnt/usr/lib/libgcc_s.so.1 /mnt/usr/lib/libstdc++.so.6