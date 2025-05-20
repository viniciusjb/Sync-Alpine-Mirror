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

###

syncalpine.sh
#!/usr/bin/env bash

STORAGE_PATH="/home/alpine"

rsync \
  --recursive \
  --links \
  --perms \
  --times \
  --compress \
  --progress \
  --delete \
  --exclude-from='exclude.txt' \
  rsync://mirror.uepg.br/alpine/latest-stable/ \
  "$STORAGE_PATH"

---

allp.sh
#!/usr/bin/env bash

STORAGE_PATH="/home/alpine"

rsync \
  --recursive \
  --links \
  --perms \
  --times \
  --compress \
  --progress \
  --delete \
  --dry-run \
  --stats \
  --exclude-from='exclude.txt' \
  rsync://mirror.uepg.br/alpine/latest-stable/ \
  "$STORAGE_PATH"

---

exclude.txt
debug
aarch64/
armv7/
armhf/
cloud/
ppc64le/
riscv64/
s390x/

---

README.md
# Sync Alpine Repository

Este repositório contém scripts para sincronizar localmente o repositório do Alpine Linux usando rsync, focando na versão `latest-stable` e excluindo arquiteturas não desejadas.

## 📁 Arquivos

- `syncalpine.sh`: Executa a sincronização real para `/home/alpine`.
- `allp.sh`: Simula a sincronização usando `--dry-run` e mostra estatísticas detalhadas.
- `exclude.txt`: Lista de diretórios/arquiteturas a serem excluídos da sincronização.

## ⚙️ Requisitos

- `rsync`
- Permissões de escrita no diretório de destino

## 🚀 Como usar

1. Torne os scripts executáveis:

```bash
chmod +x syncalpine.sh allp.sh
```

2. Simule a sincronização:

```bash
./allp.sh
```

3. Execute a sincronização real (com `sudo` se necessário):

```bash
sudo ./syncalpine.sh
```

## 🔍 Observações

- O destino padrão é `/home/alpine`, mas você pode editar os scripts para alterar esse caminho.
- Os diretórios e arquiteturas listados em `exclude.txt` são ignorados para economizar espaço.

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).



## 🧪 Script de Simulação: `allp.sh`

Este script é uma versão de teste da sincronização, usando as opções `--dry-run` e `--stats` para simular o processo sem copiar ou excluir arquivos.

### Uso:
# 🔄 Sync Alpine – Espelho Local com rsync

Este repositório contém scripts para sincronizar ou testar a sincronização de um mirror do Alpine Linux (última versão estável) usando `rsync`.

## 📂 Scripts

### `allp.sh` – Simulação de Sincronização (`--dry-run`)
Este script simula a sincronização completa com o mirror do Alpine Linux, exibindo estatísticas detalhadas **sem copiar arquivos**.

🔧 **O que ele faz:**
- Executa o `rsync` em modo `--dry-run`, que simula a operação sem fazer alterações no sistema.
- Mostra:
  - Quais arquivos seriam baixados.
  - Tamanho total dos dados.
  - Quantidade de arquivos verificados e alterados.
- Usa opções como `--stats` e `--progress` para exibir detalhes ricos da operação.

📌 **Ideal para:**
- Testar conectividade com o servidor rsync.
- Avaliar o tamanho estimado do download.
- Verificar se o mirror remoto está disponível e responsivo.

📁 **Caminho de destino (simulado):** `/home/alpine`

### `syncalpine.sh` – Sincronização Real
Este script realiza a sincronização real com os mesmos parâmetros do `allp.sh`, mas **efetivamente baixa os arquivos** para `/home/alpine`.

### `testspeed.sh` – Teste de Velocidade
Utiliza `/dev/null` como destino para testar a **velocidade de download** do mirror.

---

## 🛠️ Como Usar

1. Torne os scripts executáveis:
   ```bash
   chmod +x allp.sh syncalpine.sh testspeed.sh

```bash
chmod +x allp.sh
./allp.sh



#!/usr/bin/env bash

STORAGE_PATH="/home/alpine"

rsync \
  --recursive \
  --links \
  --perms \
  --times \
  --compress \
  --progress \
  --delete \
  --dry-run \
  --stats \
  --exclude='debug' \
  --exclude='armv7' \
  --exclude='aarch64' \
  --exclude='aarch64/' \
  --exclude='armhf/' \
  --exclude='armv7/' \
  --exclude='cloud/' \
  --exclude='ppc64le/' \
  --exclude='riscv64/' \
  --exclude='s390x/' \
  rsync://mirror.uepg.br/alpine/latest-stable/ \
  "$STORAGE_PATH"



A lista de arquivos e pastas excluídas está embutida nos scripts ou pode ser mantida separadamente no arquivo exclude.txt:
em lua


debug
aarch64
aarch64/
armv7
armv7/
armhf/
cloud/
ppc64le/
riscv64/
s390x/


#apache config no debian

# ⚙️ Configuração Principal do Apache2 no Debian

Este repositório contém uma cópia comentada do arquivo `apache2.conf`, que é o principal arquivo de configuração do servidor web Apache2 em sistemas Debian e derivados.

## 📄 Sobre `apache2.conf`

O arquivo `apache2.conf` é responsável por **orquestrar toda a configuração do Apache2**. Ele inclui diretivas globais e carrega configurações adicionais de outros arquivos e diretórios.

### 🗂️ Estrutura da Configuração no Debian

O Debian organiza os arquivos de configuração do Apache da seguinte maneira:


### 🔄 Como os arquivos são ativados

- **a2enmod / a2dismod**: ativa/desativa módulos.
- **a2ensite / a2dissite**: ativa/desativa VirtualHosts.
- **a2enconf / a2disconf**: ativa/desativa fragmentos de configuração.

> Esses comandos criam/removem links simbólicos para os diretórios `*-enabled/`.

---

## 🔧 Principais Diretivas em `apache2.conf`

| Diretiva                  | Descrição                                                                 |
|--------------------------|---------------------------------------------------------------------------|
| `Timeout`                | Tempo máximo de espera por conexões.                                     |
| `KeepAlive`              | Mantém conexões persistentes ativas.                                     |
| `MaxKeepAliveRequests`   | Número máximo de requisições por conexão persistente.                    |
| `PidFile`                | Define onde o Apache grava o PID do processo.                            |
| `User` e `Group`         | Usuário e grupo sob os quais o Apache será executado.                    |
| `ErrorLog`               | Caminho para o arquivo de log de erros.                                  |
| `LogLevel`               | Nível de detalhamento dos logs.                                          |
| `AccessFileName`         | Define o nome do arquivo `.htaccess`.                                    |

---

## 📁 Permissões de Diretórios

O Apache por padrão **nega acesso a tudo** (`<Directory />`) e libera apenas:

- `/usr/share`
- `/var/www`
- `/srv` (se estiver em uso local)

Exemplo ativo:
```apache
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>

# Verificar se a configuração está correta
apachectl configtest

# Reiniciar o Apache após alterações
systemctl restart apache2

# Ver logs de erros
tail -f /var/log/apache2/error.log

 Observações
O Apache no Debian não deve ser iniciado diretamente com /usr/bin/apache2.

Use sempre systemctl, apache2ctl ou /etc/init.d/apache2.

apache2.conf

::
#arquivo do apache2.conf

um readme para root\@bruto:/etc/apache2# cat apache2.conf

# This is the main Apache server configuration file.  It contains the

# configuration directives that give the server its instructions.

# See [http://httpd.apache.org/docs/2.4/](http://httpd.apache.org/docs/2.4/) for detailed information about

# the directives and /usr/share/doc/apache2/README.Debian about Debian specific

# hints.

#

#

# Summary of how the Apache 2 configuration works in Debian:

# The Apache 2 web server configuration in Debian is quite different to

# upstream's suggested way to configure the web server. This is because Debian's

# default Apache2 installation attempts to make adding and removing modules,

# virtual hosts, and extra configuration directives as flexible as possible, in

# order to make automating the changes and administering the server as easy as

# possible.

# It is split into several files forming the configuration hierarchy outlined

# below, all located in the /etc/apache2/ directory:

#

# /etc/apache2/

# |-- apache2.conf

# |       \`--  ports.conf

# |-- mods-enabled

# |       |-- \*.load

# |       \`-- \*.conf

# |-- conf-enabled

# |       \`-- \*.conf

# \`-- sites-enabled

# \`-- \*.conf

#

#

# \* apache2.conf is the main configuration file (this file). It puts the pieces

# together by including all remaining configuration files when starting up the

# web server.

#

# \* ports.conf is always included from the main configuration file. It is

# supposed to determine listening ports for incoming connections which can be

# customized anytime.

#

# \* Configuration files in the mods-enabled/, conf-enabled/ and sites-enabled/

# directories contain particular configuration snippets which manage modules,

# global configuration fragments, or virtual host configurations,

# respectively.

#

# They are activated by symlinking available configuration files from their

# respective \*-available/ counterparts. These should be managed by using our

# helpers a2enmod/a2dismod, a2ensite/a2dissite and a2enconf/a2disconf. See

# their respective man pages for detailed information.

#

# \* The binary is called apache2. Due to the use of environment variables, in

# the default configuration, apache2 needs to be started/stopped with

# /etc/init.d/apache2 or apache2ctl. Calling /usr/bin/apache2 directly will not

# work with the default configuration.

# Global configuration

#

#

# ServerRoot: The top of the directory tree under which the server's

# configuration, error, and log files are kept.

#

# NOTE!  If you intend to place this on an NFS (or otherwise network)

# mounted filesystem then please read the Mutex documentation (available

# at [URL\:http://httpd.apache.org/docs/2.4/mod/core.html#mutex](URL:http://httpd.apache.org/docs/2.4/mod/core.html#mutex));

# you will save yourself a lot of trouble.

#

# Do NOT add a slash at the end of the directory path.

#

\#ServerRoot "/etc/apache2"

#

# The accept serialization lock file MUST BE STORED ON A LOCAL DISK.

#

\#Mutex file:\${APACHE\_LOCK\_DIR} default

#

# The directory where shm and other runtime files will be stored.

#

DefaultRuntimeDir \${APACHE\_RUN\_DIR}

#

# PidFile: The file in which the server should record its process

# identification number when it starts.

# This needs to be set in /etc/apache2/envvars

#

PidFile \${APACHE\_PID\_FILE}

#

# Timeout: The number of seconds before receives and sends time out.

#

Timeout 300

#

# KeepAlive: Whether or not to allow persistent connections (more than

# one request per connection). Set to "Off" to deactivate.

#

KeepAlive On

#

# MaxKeepAliveRequests: The maximum number of requests to allow

# during a persistent connection. Set to 0 to allow an unlimited amount.

# We recommend you leave this number high, for maximum performance.

#

MaxKeepAliveRequests 100

#

# KeepAliveTimeout: Number of seconds to wait for the next request from the

# same client on the same connection.

#

KeepAliveTimeout 5

# These need to be set in /etc/apache2/envvars

User \${APACHE\_RUN\_USER}
Group \${APACHE\_RUN\_GROUP}

#

# HostnameLookups: Log the names of clients or just their IP addresses

# e.g., [www.apache.org](http://www.apache.org) (on) or 204.62.129.132 (off).

# The default is off because it'd be overall better for the net if people

# had to knowingly turn this feature on, since enabling it means that

# each client request will result in AT LEAST one lookup request to the

# nameserver.

#

HostnameLookups Off

# ErrorLog: The location of the error log file.

# If you do not specify an ErrorLog directive within a <VirtualHost>

# container, error messages relating to that virtual host will be

# logged here.  If you *do* define an error logfile for a <VirtualHost>

# container, that host's errors will be logged there and not here.

#

ErrorLog \${APACHE\_LOG\_DIR}/error.log

#

# LogLevel: Control the severity of messages logged to the error\_log.

# Available values: trace8, ..., trace1, debug, info, notice, warn,

# error, crit, alert, emerg.

# It is also possible to configure the log level for particular modules, e.g.

# "LogLevel info ssl\:warn"

#

LogLevel warn

# Include module configuration:

IncludeOptional mods-enabled/*.load
IncludeOptional mods-enabled/*.conf

# Include list of ports to listen on

Include ports.conf

# Sets the default security model of the Apache2 HTTPD server. It does

# not allow access to the root filesystem outside of /usr/share and /var/[www](http://www).

# The former is used by web applications packaged in Debian,

# the latter may be used for local directories served by the web server. If

# your system is serving content from a sub-directory in /srv you must allow

# access here, or in any related virtual host.

<Directory />
        Options FollowSymLinks
        AllowOverride None
        Require all denied
</Directory>

\<Directory /usr/share>
AllowOverride None
Require all granted </Directory>

\<Directory /var/www/>
Options Indexes FollowSymLinks
AllowOverride None
Require all granted </Directory>

\<Directory /srv/>
Options Indexes FollowSymLinks
AllowOverride None
Require all granted </Directory>

\#DocumentRoot /home/
\#\<Directory /home/>

# Options Indexes FollowSymLinks

# AllowOverride None

# Require all granted

\#</Directory>

# AccessFileName: The name of the file to look for in each directory

# for additional configuration directives.  See also the AllowOverride

# directive.

#

AccessFileName .htaccess

#

# The following lines prevent .htaccess and .htpasswd files from being

# viewed by Web clients.

#

\<FilesMatch "^.ht">
Require all denied </FilesMatch>

#

# The following directives define some format nicknames for use with

# a CustomLog directive.

#

# These deviate from the Common Log Format definitions in that they use %O

# (the actual bytes sent including headers) instead of %b (the size of the

# requested file), because the latter makes it impossible to detect partial

# requests.

#

# Note that the use of %{X-Forwarded-For}i instead of %h is not recommended.

# Use mod\_remoteip instead.

#

LogFormat "%v:%p %h %l %u %t "%r" %>s %O "%{Referer}i" "%{User-Agent}i"" vhost\_combined
LogFormat "%h %l %u %t "%r" %>s %O "%{Referer}i" "%{User-Agent}i"" combined
LogFormat "%h %l %u %t "%r" %>s %O" common
LogFormat "%{Referer}i -> %U" referer
LogFormat "%{User-agent}i" agent

# Include of directories ignores editors' and dpkg's backup files,

# see README.Debian for details.

# Include generic snippets of statements

IncludeOptional conf-enabled/\*.conf

# Include the virtual host configurations:

IncludeOptional sites-enabled/\*.conf

