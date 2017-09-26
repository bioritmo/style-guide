# Recomendações gerais

Sigam estas recomendações independentemente da linguagem utilizada no seu código fonte - desde Ruby até HTML ou Markdown, estas práticas básicas devem ser seguidas. O melhor jeito de seguir estas recomendações é configurar o seu editor para fazer o trabalho pesado para você.

* Não deixe espaços em branco no fim das linhas:
    * No Vim você pode adicionar algo como `autocmd BufWritePre * :%s/\s\+$//e` no seu `~/.vimrc`.
    * No Sublime Text você pode setar ```trim_trailing_white_space_on_save``` para ```true```.
    * No Atom o pacote `whitespace` já está habilitado por padrão.

* Tab size e indentação: Use 2 espaços em vez de tabs para indentação.
    * No Vim: edite seu ```~/.vimrc``` e adicione ```set sw=2```, ```set sts=2```, ```set expandtab``` e ```set autoindent```.
    * No Sublime Text: edite as preferências de usuário (⌘ + ,) e mude ```tab_size``` para ```2```, ```translate_tabs_to_spaces``` para ```true``` e ```use_tab_stops``` to ```true```.
    * No Atom: por default já está assim, mas são as opções `Tab Length: 2`, `Soft Tabs: true` e `Tab Type: auto`.

* Evite linhas muito longas, independentemente da quebra de linha que o seu editor faz. Mantenha seu código sucinto e legível.
