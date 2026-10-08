# Como instalar/configurar/usar o `mousetrail` no `Linux Ubuntu`

## Resumo

Este guia explica como clonar o repositório `OneTrueC/mouseTrail`, compilar o `mousetrail` com as bibliotecas do `X11` e configurá-lo para iniciar automaticamente na sessão gráfica do `Linux Ubuntu`.

## _Abstract_

_This guide explains how to clone the `OneTrueC/mouseTrail` repository, build `mousetrail` with the `X11` libraries, and configure it to start automatically in a `Linux Ubuntu` graphical session._

## Descrição

### `mousetrail`

O `mousetrail` é um programa escrito em `C` que cria um rastro visual para o ponteiro do _mouse_ usando o sistema de janelas `X11`. O código-fonte permite habilitar um efeito de arco-íris e configurar a quantidade e o intervalo das cópias do ponteiro.

## Pré-requisitos

- Uma sessão gráfica `X11`. O programa usa `Xlib` e `Xfixes`; não há suporte declarado a sessões `Wayland`.
- Permissão para usar `sudo` para instalar as dependências e o executável em `/usr/local`.
- Conexão com a _internet_ para acessar os repositórios do `Linux Ubuntu` e o `GitHub`.
- O diretório `~/mouseTrail` ainda não deve existir antes da clonagem inicial.

## 1. Abrir o `Terminal Emulator`

1. Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando:
        
    ```bash
    sudo apt clean
    ```

    2.2 Remover pacotes `.deb` antigos ou duplicados do `cache` local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando:

    ```bash
    sudo apt autoclean
    ```

    2.3 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando:

    ```bash
    sudo apt autoremove -y
    ```

    2.4 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`:

    ```bash
    sudo apt update
    ```

    2.5 **Corrigir pacotes quebrados**: Isso atualizará a lista de pacotes disponíveis e tentará corrigir pacotes quebrados ou com dependências ausentes:

    ```bash
    sudo apt --fix-broken install
    ```

    2.6 Limpar o `cache` do gerenciador de pacotes `apt` novamente:

    ```bash
    sudo apt clean
    ```

    2.7 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:

    ```bash
    sudo apt list --upgradable
    ```

    2.8 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update`. Digite o seguinte comando e pressione `Enter`:

    ```bash
    sudo apt full-upgrade -y
    ```


## 3. Instalar as dependências e compilar o `mousetrail`

1. Instalar o `Git`, o compilador `C` e os arquivos de desenvolvimento de `X11` e `Xfixes`:

    ```bash
    sudo apt install git build-essential libx11-dev libxext-dev libxfixes-dev -y
    ```

2. Clonar o repositório oficial em `~/mouseTrail`:

    ```bash
    git clone https://github.com/OneTrueC/mouseTrail.git "$HOME/mouseTrail"
    ```

3. Compilar o programa no diretório clonado:

    ```bash
    make -C "$HOME/mouseTrail"
    ```

4. Instalar o executável e a página de manual em `/usr/local`:

    ```bash
    cd "$HOME/mouseTrail"
    sudo mkdir -p /usr/local/bin /usr/local/share/man/man1
    sudo make install
    ```

5. Confirmar o caminho do executável:

    ```bash
    command -v mousetrail
    ```

O `Makefile` do projeto instala o executável em `/usr/local/bin/mousetrail`.

## 1.1 Código completo para configurar/instalar/usar

Para clonar, compilar, instalar e configurar o início automático do `mousetrail` no `Linux Ubuntu`, seguir estas etapas:

1. Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Digitar o bloco completo a seguir e pressionar `Enter`:

    ```bash
    sudo apt clean
    sudo apt autoclean
    sudo apt autoremove -y
    sudo apt update
    sudo apt --fix-broken install
    sudo apt clean
    sudo apt list --upgradable
    sudo apt full-upgrade -y
    sudo apt install git build-essential libx11-dev libxext-dev libxfixes-dev -y
    git clone https://github.com/OneTrueC/mouseTrail.git "$HOME/mouseTrail"
    make -C "$HOME/mouseTrail"
    cd "$HOME/mouseTrail"
    sudo mkdir -p /usr/local/bin /usr/local/share/man/man1
    sudo make install
    mkdir -p "$HOME/.config/autostart"
    cat > "$HOME/.config/autostart/mousetrail.desktop" <<'EOF'
    [Desktop Entry]
    Type=Application
    Name=MouseTrail
    Comment=Rastro visual do ponteiro do mouse
    Exec=/usr/local/bin/mousetrail
    Terminal=false
    X-GNOME-Autostart-enabled=true
    EOF
    command -v mousetrail
    ```

O bloco de instalação pressupõe que `~/mouseTrail` ainda não exista. Se o programa já tiver sido clonado, executar a compilação e a instalação a partir desse diretório, sem repetir `git clone`.

## 4. Configurar a inicialização automática

### 4.1 Ativar o `mousetrail`

O arquivo `.desktop` em `~/.config/autostart/` inicia o programa quando o ambiente gráfico abrir a sessão do usuário.

1. Criar o diretório de _autostart_:

    ```bash
    mkdir -pv "$HOME/.config/autostart"
    ```

2. Criar o arquivo _desktop_ para o `mousetrail`:

    ```bash
    touch mousetrail
    ```

3. Abrir o arquivo com o `nano`:

    ```bash
    sudo nano mousetrail
    ```

4. Inserir o conteúdo dentro do arquivo `~/.config/autostart/mousetrail.desktop`:

    ```bash
    [Desktop Entry]
    Type=Application
    Name=mouseTrail
    Comment=Cursor mouse trail
    Exec=/home/edenedfsls/Documents/Downloads/unix/ubuntu/mousetrail/docs/mouseTrail
    Terminal=false
    Hidden=false
    X-GNOME-Autostart-enabled=true
    ```

5. Iniciar o programa manualmente para confirmar que a sessão gráfica consegue executá-lo:

    ```bash
    gtk-launch mousetrail
    ```

    O programa permanece ativo enquanto cria o rastro. Pressionar `Ctrl + C` no `Terminal Emulator` para encerrá-lo. No próximo início de sessão gráfica, o ambiente deverá iniciá-lo pelo arquivo de _autostart_.

6. Executar o `autostart` imediatamente. Utilize:

    ```bash
    gio launch "$HOME/.config/autostart/mousetrail.desktop"
    ```

    Esse comando executa o aplicativo definido no arquivo `.desktop`, simulando sua inicialização, sem precisar reiniciar o sistema.

7. Verificar se está executando, com o comando:

    ```bash
    pgrep -af mousetrail
    ```
    
    Ou apenas arraste o _mouse_ e verifique se o rastro aparece.

8. Encerrar quando desejar:

    ```bash
    pkill -x mousetrail
    ```

**Observação**: o `gio launch` executa somente esse aplicativo, não reinicia todo o mecanismo de `autostart` do `XFCE`.
Se funcionar, o mesmo arquivo em `~/.config/autostart/` deverá iniciar o `mousetrail` automaticamente no próximo _login_.

### 4.2 Desativar o `mousetrail`

1. Para impedir que ele inicie automaticamente, remover a entrada:

    ```bash
    rm "$HOME/.config/autostart/mousetrail.desktop"
    ```

## Compatibilidade e observações

- O projeto depende de uma sessão `X11`, dos arquivos de desenvolvimento `libx11-dev` e `libxfixes-dev`, e de um compilador C.
- A compilação produz o executável `mousetrail`; o `Makefile` instala o binário e a página de manual em `/usr/local`.
- O `autostart` é configurado somente para o usuário atual e executa o binário instalado em `/usr/local/bin/mousetrail`.
- O projeto não publica uma medição de consumo de recursos. Comparar o uso de CPU e memória no ambiente local antes de decidir manter a inicialização automática.

## Licença e suporte

O repositório upstream inclui a licença `GNU GPL` versão 3 ou posterior. Consultar o arquivo `LICENSE` distribuído com o código-fonte.

Para relatar problemas ou consultar o código, acessar `OneTrueC/mouseTrail` no `GitHub`.

## Referências

[1] OPENAI.
**Instalar o `mousetrail` no `linux ubuntu` pelo `terminal emulator`**.
Disponível em: <https://chatgpt.com/g/g-p-6980caf949648191ad6acfcdbe590f9e-instalar/c/6ac754e0-d664-83ea-906a-50fab09b9f73>.
ChatGPT.
Acessado em: 08/10/2026.

[2] ONETRUEC.
**Mousetrail: programa de rastro do ponteiro para `X11`**.
Disponível em: <https://github.com/OneTrueC/mouseTrail>.
GitHub.
Acessado em: 08/10/2026.

[3] UBUNTU.
**Gerenciar pacotes e instalar _software_**.
Disponível em: <https://ubuntu.com/server/docs/package-management/>.
Acessado em: 08/10/2026.

[4] FREEDESKTOP.
**Especificação de inicialização automática de aplicativos**.
Disponível em: <https://specifications.freedesktop.org/autostart/latest/>.
Acessado em: 08/10/2026.
