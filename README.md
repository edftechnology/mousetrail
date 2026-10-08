<!-- LOGOTIPO DO PROJETO -->
<div style="display: flex; justify-content: center;">
   <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">
     <img src="docs/figures/logo.png" alt="Logo" width="200" height="100">
   </a>
</div>

<h3 align="center">NomeDoProjeto</h3>

<div style="display: flex; justify-content: center;">
  <a href="https://doi.org/SEU-DOI">
    <img src="https://zenodo.org/badge/SEU_BADGE.svg" alt="DOI">
  </a>
</div>

<p align="center">
 Uma descrição curta e genérica do projeto. Substitua por um resumo real quando usar este template.
 <br />
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO"><strong>Explore os documentos »</strong></a>
 <br />
 <br />
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">Ver demonstração</a>
 ·
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">Relatar bug</a>
 ·
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">Solicitar recurso</a>
</p>




# Como instalar/configurar/usar o `mousetrail` no `Linux Ubuntu`

## Resumo

Este guia apresenta como procurar e instalar o `mousetrail` pelo `apt` no `Linux Ubuntu`, verificar a instalação e iniciar o programa.

## _Abstract_

_This guide explains how to find and install `mousetrail` with `apt` on `Linux Ubuntu`, verify the installation, and launch the program._

## Descrição

### `mousetrail`

O `mousetrail` cria um rastro visual para o ponteiro do mouse no sistema de janelas `X11` e pode aplicar um efeito de arco-íris. O projeto upstream é disponibilizado como código-fonte no GitHub.

## Pré-requisitos

- Usar uma sessão gráfica baseada em `X11`; o projeto não declara suporte a sessões `Wayland`.
- Ter permissão para usar `sudo`.
- Ter os repositórios oficiais do `Linux Ubuntu` configurados e acesso à internet.
- O pacote precisa estar disponível nas fontes `apt` habilitadas para a versão instalada do `Linux Ubuntu`.

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

## 3. Procurar o pacote `mousetrail`

Antes de instalar, verificar se o pacote está nos repositórios habilitados para a versão do `Linux Ubuntu` em uso.

1. Atualizar o índice de pacotes e procurar o nome exato:

    ```bash
    sudo apt update
    apt search '^mousetrail$'
    apt policy mousetrail
    ```

2. Se `apt policy mousetrail` mostrar um candidato, instalar o pacote:

    ```bash
    sudo apt install mousetrail -y
    ```

3. Se não houver candidato e a busca não listar o pacote, os repositórios `apt` configurados não fornecem `mousetrail`. Não instalar `gnome-mousetrap` como substituto: é outro aplicativo, voltado ao controle do ponteiro por movimentos da cabeça. Consulte a página upstream indicada em **Referências** para verificar as opções disponibilizadas pelo desenvolvedor.

## 1.1 Código completo para configurar/instalar/usar

Para instalar o `mousetrail` no `Linux Ubuntu` quando o pacote estiver disponível nos repositórios configurados, seguir estas etapas:

1. Abrir o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Digitar os comandos a seguir e pressionar `Enter`:

    ```bash
    sudo apt update
    apt policy mousetrail
    sudo apt install mousetrail -y
    mousetrail
    ```

Se `apt policy` não apresentar um candidato, não há instalação pelo `apt` com as fontes configuradas.

## 4. Executar e verificar o `mousetrail`

1. Iniciar o programa em uma sessão `X11` com o comando:

    ```bash
    mousetrail
    ```

2. Para verificar se o comando está instalado, executar:

    ```bash
    command -v mousetrail
    apt policy mousetrail
    ```

O programa depende de uma conexão com o servidor `X`; se não conseguir conectar, confirmar se a sessão gráfica atual usa `X11`.

## Compatibilidade

- A disponibilidade do pacote deve ser confirmada para cada versão e conjunto de repositórios do `Linux Ubuntu`.
- O `mousetrail` upstream usa o sistema de janelas `X11`.
- `gnome-mousetrap` é um pacote diferente e não implementa o mesmo rastro visual do ponteiro.

## Licença

Este repositório inclui o arquivo `LICENSE.txt`.

## Contato e suporte

Para dúvidas ou problemas, consultar o repositório upstream `OneTrueC/mouseTrail` e a documentação da versão instalada do `Linux Ubuntu`.

## Referências

[1] OPENAI. **Instalar o `mousetrail` no `linux ubuntu` pelo `terminal emulator`**. Disponível em: <https://chatgpt.com/g/g-p-6980caf949648191ad6acfcdbe590f9e-instalar/c/6ac754e0-d664-83ea-906a-50fab09b9f73>. ChatGPT. Acessado em: 08/10/2026.

[2] ONETRUEC. **mousetrail**. Disponível em: <https://github.com/OneTrueC/mouseTrail>. Acessado em: 08/10/2026.

[3] UBUNTU. **Gerenciar pacotes e instalar software**. Disponível em: <https://ubuntu.com/server/docs/package-management/>. Acessado em: 08/10/2026.

[4] UBUNTU. **Pesquisa de pacotes do Ubuntu**. Disponível em: <https://packages.ubuntu.com/search?keywords=mousetrail>. Acessado em: 08/10/2026.

<!-- LICENÇA -->
## Licença

Distribuído sob a licença `MIT`. Consulte `LICENSE.txt` para obter mais informações.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>



<!-- ROTEIRO -->
## Roteiro

- [ ] Adicionar registro de alterações
- [ ] Adicionar links de volta ao topo
- [ ] Adicionar modelos adicionais com exemplos
- [ ] Suporte multilíngue

Consulte os problemas abertos para obter uma lista completa dos recursos propostos.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>




<!-- CONTRIBUIÇÔES -->
## Contribuições

Explique como contribuir (fork, branch, PR, issues).

1. Bifurque o projeto
2. Crie sua ramificação (`git checkout -b feature/NovaFuncionalidade`)
3. Confirme suas alterações (`git commit -m 'Describe change'`)
4. Envie para a filial (`git push origin feature/NovaFuncionalidade`)
5. Abra uma solicitação `pull`

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>




<!-- ACKNOWLEDGMENTS -->
## Agradecimentos

* [Best README Template](https://github.com/othneildrew/Best-README-Template?tab=readme-ov-file)

* [Choose an Open Source License](https://choosealicense.com)

* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)

* [Malven's Flexbox Cheatsheet](https://flexbox.malven.co/)

* [Malven's Grid Cheatsheet](https://grid.malven.co/)

* [Img Shields](https://shields.io)

* [GitHub Pages](https://pages.github.com)

* [Font Awesome](https://fontawesome.com)

* [React Icons](https://react-icons.github.io/react-icons/search)

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>
