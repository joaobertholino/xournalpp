# Configuração Xournal++

Este repositório é o submódulo `xournalpp` do projeto de dotfiles. Ele armazena preferências do Xournal++, modelos de página, uma paleta Dracula e a barra de ferramentas; não inclui o aplicativo Xournal++.

## Instalação

1. Instale o Xournal++ pelo método da sua distribuição.
2. Inicialize o submódulo a partir do repositório principal ou clone este repositório diretamente em `~/.config/xournalpp`:

   ```bash
   git submodule update --init --recursive .config/xournalpp
   ```

3. Feche o Xournal++ antes de substituir os arquivos e faça backup da configuração existente:

   ```bash
   cp -a "$HOME/.config/xournalpp" "$HOME/xournalpp-backup-$(date +%Y%m%d-%H%M%S)"
   ```

As configurações podem ser alteradas pelo próprio aplicativo. `settings.xml` informa explicitamente que a maior parte das opções deve ser ajustada pela janela de configurações; edite-o à mão somente com o aplicativo fechado.

## Arquivos

| Arquivo/diretório | Finalidade |
| --- | --- |
| `settings.xml` | Preferências da interface, dispositivos, páginas, cores, LaTeX e autosave. |
| `toolbar.ini` | Barra de ferramentas de anotação. |
| `palettes/Dracula.gpl` | Paleta Dracula versionada. |
| `page-models/A4-page.xopt` e `small-page.xopt` | Modelos de página. |
| `print-config.ini` | Últimas preferências de impressão/exportação. |

## Comportamento configurado

- Tema escuro forçado, ícones Lucide, janela maximizada e barra lateral inicialmente oculta.
- Autosave ativado com intervalo de 1 (unidade controlada pelo Xournal++).
- Rolagem ilimitada e página nova em fundo quadriculado/preto.
- Pressão de caneta ativada; ferramentas padrão com caneta branca muito fina, marca-texto roxo e borracha muito fina.
- Áudio desativado.
- Barra de ferramentas com caneta, borracha, laser, cores, desfazer/refazer, zoom, páginas e controles de áudio.
- Suporte a LaTeX configurado para executar `pdflatex -halt-on-error -interaction=nonstopmode '{}'`.

## Dependências e itens opcionais

| Funcionalidade | Requisito observado |
| --- | --- |
| Uso básico | Xournal++ |
| Inserções LaTeX | `pdflatex` e as dependências que a instalação do Xournal++ identificar |
| Dispositivos de caneta | Dispositivos compatíveis configurados no sistema |

O repositório não especifica nomes de pacotes do sistema nem instala o TeX Live. A paleta `Dracula.gpl` é fornecida pelo próprio repositório; `settings.xml` ainda aponta a paleta ativa para `/usr/share/xournalpp/palettes/xournalpp.gpl`, portanto selecione Dracula no aplicativo se desejar torná-la ativa.

## Ajustes locais obrigatórios

Revise ou limpe preferências que pertencem à máquina original:

- `lastSavePath` e `lastOpenPath`: `/home/joaob/Mathematics/Areas/Metric-Spaces`;
- `lastImagePath`: `/home/joaob/Downloads`;
- destino de impressão: `/home/joaob/saída.pdf` em `print-config.ini`;
- tamanho/estado da janela (`1918×1056`, maximizada);
- dispositivos conhecidos, incluindo `OpenTabletDriver Virtual Artist Tablet` e variantes de `Wacom One by Wacom S Pen`.

Essas referências não impedem o Xournal++ de abrir, mas podem apontar para diretórios ou dispositivos inexistentes em outro sistema.

## Atualização e rollback

Não há instalador, atualizador ou desinstalador. Para atualizar a cópia Git:

```bash
git pull --ff-only
```

Para rollback, feche o Xournal++, restaure o diretório de backup criado antes da instalação e abra o aplicativo novamente. Como os diretórios são copiados/mesclados, não há um comando de remoção seguro fornecido por este repositório.
