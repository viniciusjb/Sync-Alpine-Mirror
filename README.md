# Sync-Alpine-Mirror
Este repositório contém um script simples para sincronizar o mirror do Alpine Linux latest-stable em um diretório local usando rsync.

---

## Pré-requisitos

* `bash` (shell compatível)
* `rsync` instalado no sistema

## Estrutura do repositório

```
syncalpine.sh  # Script principal para sincronização
exclude.txt    # Lista de padrões a serem excluídos (opcional)
```

---

## Script: `syncalpine.sh`

```bash
#!/usr/bin/env bash

# Diretório onde o mirror será armazenado
STORAGE_PATH="/home/alpine"

rsync \
  --recursive \   # Recursivo, copia diretórios e subdiretórios
  --links \       # Preserva links simbólicos
  --perms \       # Preserva permissões
  --times \       # Preserva timestamps
  --compress \    # Comprime dados durante a transferência
  --progress \    # Exibe progresso
  --delete \      # Remove arquivos locais não mais existentes na origem
  --exclude-from='exclude.txt' \  # Lista de padrões para excluir
  rsync://mirror.uepg.br/alpine/latest-stable/ \
  "${STORAGE_PATH}"
```

> **Nota:** Se você não quiser usar o arquivo `exclude.txt`, substitua a opção `--exclude-from` por múltiplas opções `--exclude`:
>
> ```bash
> --exclude='debug/' \
> --exclude='armv7/' \
> --exclude='aarch64/' \
> --exclude='armhf/' \
> --exclude='cloud/' \
> --exclude='ppc64le/' \
> --exclude='riscv64/' \
> --exclude='s390x/' \
> ```

---

## Arquivo de exclusões: `exclude.txt`

Liste aqui todos os diretórios ou padrões que não devem ser sincronizados. Por exemplo:

```
debug/
armv7/
aarch64/
armhf/
cloud/
ppc64le/
riscv64/
s390x/
```

---

## Boas práticas

* **Aspas em variáveis:** Utilize sempre `"${VAR}"` para evitar problemas com espaços no caminho.
* **Manutenção de exclusões:** Centralize padrões de exclusão em `exclude.txt` para facilitar futuras alterações.

---

## Uso

1. Atualize o caminho em `STORAGE_PATH` para o diretório desejado.
2. Se necessário, ajuste os padrões em `exclude.txt`.
3. Dê permissão de execução ao script:

   ```bash
   chmod +x syncalpine.sh
   ```
4. Execute:

   ```bash
   ./syncalpine.sh
   ```

---

*Desenvolvido por Vinícius — 2025*
