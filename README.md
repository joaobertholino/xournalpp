# Xournal++ — configuração pessoal no Gentoo

Submódulo de [dotfiles](https://github.com/joaobertholino/dotfiles), instalado em `~/.config/xournalpp`. Contém preferências, barras de ferramentas, paletas e modelos; o aplicativo Xournal++ é instalado separadamente. Conferido em **25/10/2026**.

## Arquivos

| Arquivo/diretório | Função |
| --- | --- |
| `settings.xml` | Interface, caneta, cores, dispositivos, autosave e LaTeX |
| `toolbar.ini` | Barras de ferramentas de anotação |
| `palette.gpl` | Cópia local da paleta padrão do Xournal++ |
| `palettes/Dracula.gpl` | Paleta Dracula adicional |
| `page-models/` | Modelos de página A4 e pequena |
| `print-config.ini` | Preferências locais de impressão/exportação |

## Preferências atuais

- Interface em português brasileiro, tema escuro forçado e ícones Lucide.
- Barra selecionada: `Right hand Note Taking Copy`.
- Pressão da caneta habilitada; caneta branca `VERY_FINE`, marca-texto roxo e borracha `VERY_FINE`.
- Autosave habilitado, com `autosaveTimeout=1` no arquivo de preferências.
- Áudio desativado, rolagem ilimitada desativada e encaixe de rotação desativado.
- Janela gravada com `1078 × 1898`, sem maximização; o aplicativo pode atualizar esses valores durante o uso.
- Inserções LaTeX com `pdflatex -halt-on-error -interaction=nonstopmode '{}'`.

A paleta ativa em `settings.xml` ainda aponta para `/usr/share/xournalpp/palettes/xournalpp.gpl`. As paletas versionadas são alternativas: selecione-as no aplicativo se quiser mudar a paleta ativa.

## Instalação e aplicação

Instale o Xournal++ pelo método da distribuição. **Feche o aplicativo antes de substituir ou editar suas preferências**: ele pode gravar os arquivos ao encerrar.

No clone do repositório principal:

```sh
git submodule update --init --recursive .config/xournalpp
```

Para uma instalação independente, faça backup do destino e clone apenas quando `~/.config/xournalpp` não existir:

```sh
git clone git@github.com:joaobertholino/xournalpp.git "$HOME/.config/xournalpp"
```

As URLs SSH exigem autenticação no GitHub. Não copie o arquivo `.git` de um submódulo para outro diretório: ele pode apontar para metadados que só existem no clone original.

## Particularidades da máquina Gentoo

O launcher local `/usr/local/bin/xournalpp` utiliza `/usr/bin/xournalpp` com GTK nativo e `GDK_BACKEND=x11` via XWayland. Ele também limpa variáveis gráficas específicas da pilha Nix para evitar conflitos. Esse wrapper é externo ao repositório; não é requisito universal do Xournal++.

Para inserir LaTeX, o sistema precisa de `pdflatex` e dos arquivos de suporte indicados pelo aplicativo. A configuração usa o template `/usr/share/xournalpp/resources/legacy_template.tex`, que precisa existir na instalação de destino.

Revise os valores pessoais antes de usar em outra máquina:

- `lastSavePath=/home/joaob/.config/xournalpp`;
- `lastOpenPath=/home/joaob` e `lastImagePath=/home/joaob/Downloads`;
- destino de impressão em `print-config.ini`;
- dispositivos Wacom, OpenTabletDriver e XWayland gravados nas preferências;
- tamanho da janela, barra selecionada e caminhos de paleta/template.

Prefira alterar opções pela interface do Xournal++; edições manuais devem ser feitas com o programa fechado.

## Versionamento

A cópia local utiliza a branch `main` e o remoto `personal`. O script `~/.local/bin/auto-push.sh` do projeto principal salva e envia este submódulo antes de atualizar sua referência no pai. O agendamento é horário, pelo systemd do usuário.

Para conferir mudanças sem publicá-las:

```sh
git -C "$HOME/.config/xournalpp" status --short
git -C "$HOME/.config/xournalpp" diff
```

Para manutenção manual, publique primeiro as alterações deste repositório e depois atualize o gitlink no `dotfiles`. Antes de executar `git pull --ff-only`, salve as alterações do aplicativo e confira se está em uma branch. Para recuperação, feche o Xournal++ e restaure um backup ou uma versão conhecida dos arquivos.
