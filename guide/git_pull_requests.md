# Git e Pull Requests

## Git

* Sempre use o email da empresa para commits nos projetos;

### Branches

* Crie branches para todos os seus trabalhos;
* Em alguns projetos, o commit direto na master é bloqueado, então recomendamos nunca fazer isso;
* Use um [gitignore global para ignorar](https://help.github.com/articles/ignoring-files) arquivos que são específicos ao seu ambiente (configurações de editor, arquivos de sistema indesejados - por exemplo `.DS_Store` no Mac, `*.swp` do vim, etc.);
* Nomeie seus branches usando `-` para separar as palavras;
* Prefixe seus branches de acordo com o tipo de trabalho: `feature/nome-da-feature`, `bug/nome-do-bug-fix` e assim por diante;

```shell
  git checkout -b feature/crud-de-user
```

* Quando precisar atualizar a sua branch com a master, é preferível primeiro atualizar a master com `rebase`, e depois fazer merge com a sua branch;

```shell
  $ git checkout master
  $ git pull --rebase
  $ git checkout feature/minha-feature
  $ git merge master
```

* Quando for mergear sua branch na master, em geral você vai querer usar a interface de Pull Request do Github. Mais sobre isso abaixo;
* Apague as suas branches localmente e remotamente depois do merge;

### Commits

A mensagem de commit é uma das formas de documentação mais importantes em uma base de código. Caso um bug seja introduzido, uma boa mensagem de commit facilita a identificação de onde/quando isso aconteceu, e principalmente o porquê daquela alteração ter sido feita.

* Escreva suas mensagens de commit em Português;
* Boas mensagens de commit incluem um resumo e outras informações se necessário; O resumo deve dar um panorama geral do commit e o texto abaixo deve incluir mais explicações (principalmente 'Por que esse commit foi necessário?'); não escreva simplesmente o que foi feito, isso dá para saber pelo *diff*.
* Escreva o resumo na forma imperativa, ou seja, como se completasse a seguinte frase: “Esse commit `seu resumo aqui`”. Por exemplo: "*Esse commit* `Atualiza o README com informações sobre testes`"
* A primeira linha (o resumo) deve ter no máximo 50 caracteres
* As linhas seguintes devem ter no máximo 72 caracteres
* Leia mais sobre isso [aqui](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) e [aqui](https://www.lucascaton.com.br/2017/10/16/como-escrever-mensagens-de-commits-no-git/).
* Sugestão: inclua um `.gitmessage` na sua home e configure o seu `.gitconfig` para usá-lo; a primeira linha é o resumo e o resto é o corpo do commit;

`.gitconfig`
```
[commit]
  template = ~/.gitmessage
```

`.gitmessage`
```


WHY:

*

HOW:

*

# 50-character subject line
#
# 72-character wrapped longer description.
```

## Pull Requests

Os [Pull Requests](https://help.github.com/articles/using-pull-requests) do GitHub são uma ótima forma de introduzir novas alterações em um repositório através de revisões assíncronas e discussões sobre as mudanças que você quer fazer - uma nova feature, uma correção de digitação ou um bug complexo em produção que está assombrando seu código.

Revisões assíncronas permitem compartilhar conhecimento técnico: formas mais simples de implementar o mesmo comportamento, problemas conhecidos ao usar certa biblioteca, pedir ajuda em um determinado assunto que você sabe que alguém sabe mais, ou mesmo compartilhar uma decisão de design.

Além disso, quando for feita a revisão, dúvidas vão surgir, o que faz disso a oportunidade perfeita para discutir o comportamento adequado que a sua branch vai introduzir, sobre regras de negócio envolvidas e possíveis caminhos que a sua aplicação pode seguir.

Acima de tudo, os Pull Requests são uma maneira de fazer as pessoas se sentirem conectadas e conscientes do que está acontecendo em diferentes projetos.

As seções a seguir explicam com criar, manter e mergear Pull Requests.

* [Começando com branches](#comecando-com-branches)
* [Abrindo um Pull Request](#abrindo-um-pull-request)
* [GitHub Flavored Markdown](#github-flavored-markdown)
* [Screenshots e GIFs](#screenshots-and-gifs)
* [Revisando Pull Requests](#revisando-pull-requests)
* [Seu Pull Request Revisado](#seu-pull-request-revisado)
* [Mergeando Pull Requests](#mergeando-pull-requests)

### Começando com branches

Para começar um Pull Request você vai precisar de uma branch para trabalhar nas mudanças que você vai querer introduzir na branch base. A branch base, também chamada de 'mainline' do seu repositório, é a versão atualizada/estável/deployable do seu projeto ou aplicação, que na maioria dos casos é a branch `master` do repositório (exceções devem sempre ser documentadas e justificadas). Você também pode enviar Pull Requests para outras branches no seu repositório, por exemplo quando você está contribuindo em um branch existente de uma feature maior ou uma mudança grande no seu codebase (por exemplo, uma migração de versão do Rails, ou uma nova versão do site). Nesses casos, a branch alvo vai fazer o papel da branch base no lugar da `master`.

Nomeie a sua branch de acordo com o assunto da sua mudança (ver acima em [Git](#git))

### Abrindo um Pull Request

Uma vez que tiver sua branch com alguns commits nela você pode ir para a interface do GitHub e criar um novo Pull Request no repositório em que estiver trabalhando. Para um guia visual, veja a [página de ajuda do GitHub](https://help.github.com/articles/creating-a-pull-request) sobre como abrir um Pull Request.

Uma parte importante do seu Pull Request é o título e a descrição que você vai escrever. Se sua branch tem um único commit, aquela mensagem do commit será usada para compor o título e a descrição do Pull Request, ou o GitHub vai sugerir uma versão 'humanizada' do nome da sua branch para o título (como 'Feature crud de user'), o que não ajuda muito. Na maioria dos casos você deve escrever você mesmo para mostrar o que está fazendo e o porquê. Você pode explicar a origem do bug que você está arrumando, ou detalhes da nova feature que você quer introduzir com seu Pull Request. Uma boa prática é colocar o link da história ou o link do chamado e copiar a descrição deles. Ah, escreva tudo em Português.

Em alguns repositórios, haverá um [template de Pull Request](https://help.github.com/articles/creating-a-pull-request-template-for-your-repository/) com um esqueleto básico e algumas instruções, baseadas neste style guide. [Veja um exemplo de template para este repositório](PULL_REQUEST_TEMPLATE.md).

### GitHub Flavored Markdown

As descrições de Pull Requests suportam o [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown), então tem uma porção de coisas que podem ser feitas para melhorar sua descrição de Pull Request:

Você pode fazer [referências](https://help.github.com/articles/github-flavored-markdown#references) a outras Issues e Pull Requests, do mesmo repositório ou de outro, usando o formato ```owner/repo#number```. Isso vai colocar uma referência ao seu Pull Request na Issue/PR mencionada, mas não se preocupe, ele só vai estar visível para aqueles que podem visualizar o seu repositório.

[Listas de Tarefas](https://help.github.com/articles/github-flavored-markdown#task-lists) são um ótimo jeito de mostrar as tarefas que fazem parte dos seus Pull Requests e gerenciar checklists antes de mergear suas mudanças. Isso pode ser bem útil se você abre seu Pull Request antes do trabalho estar concluído (WIP - Work In Progress). Você sempre pode [mencionar outras pessoas e times](https://help.github.com/articles/github-flavored-markdown#name-and-team-mentions-autocomplete) para pedir feedback ou ideias, e trazer pessoas de fora do projeto para contribuir na discussão.

### Screenshots e GIFs

O GitHub Flavored Markdown deixa você incluir imagens dentro da sua descrição de Pull Request, o que é extremamente útil para mostrar mudanças em uma interface. Pode ser simplesmente uma mudança de padding ou uma feature completamente nova com um GIF mostrando a utilização da interface. Mudanças de interface são bastante complexas de entender somente revisando o código fonte, e referências visuais vão ajudar na discussão de mudanças visuais que são parte do seu Pull Request.

Você pode usar ferramentas como [Cloudup](https://cloudup.com/), [CloudApp](http://getcloudapp.com/), [Skitch](http://evernote.com/skitch/), [Monosnap](https://monosnap.com/welcome) e muitas outras para hospedar seus Screenshots e GIFs, ou simplesmente arrastar e soltar o arquivo no campo `textarea` da descrição que o GitHub vai cuidar disso pra você.

Para criar GIFs facilmente de você movendo e clicando no seu browser você vai precisar de algo para gravar um vídeo e convertê-lo em um GIF. Eis algumas opções que você pode achar útil:

* [gifify](https://gist.github.com/SlexAxton/4989674) um script de Alex Sexton, baseado em QuickTime, ImageMagick e FFmpeg.
* [LICEcap](http://www.cockos.com/licecap/) app para Windows e macOS.
* [Peek](https://github.com/phw/peek) app para Linux.

### Revisando Pull Requests

"Feedback é um dos processos mais difíceis e sensíveis em grupos. É fácil ferir pessoas com críticas, mas elogios falsos também não ajudam. Elogios muitas vezes nos tornam muito confortáveis, enquanto que críticas prejudicam nossa autoestima e pode nos levar a fazer escolhas erradas."

Essa frase é perfeita para explicar a delicadeza de uma revisão de Pull Request: nem tão áspero, nem tão suave.

Nós acreditamos que para escrever a revisão mais valiosa possível, nós temos que apontar problemas acionáveis.

Temos algumas sugestões que achamos úteis:

* Procure por [code smells](http://en.wikipedia.org/wiki/Code_smell) (Da definição da Wikipedia: code smells indicam fragilidades no design que podem estar atrasando o desenvolvimento ou aumentando o risco de bugs ou falhas no futuro.) no código que podem ser removidos para evitar problemas futuros no código.
* Compartilhe, sempre que possível, soluções diferentes para o mesmo problema apontando exemplos de código. Os exemplos podem vir de outro projeto ou escritos por você somente para ilustração.
* Não tenha receio de pedir documentação quando necessário. Muitas vezes as discussões geradas por um Pull Request devem ser adicionadas ao projeto na forma de documentação, mesmo coisas relacionadas a partes específicas do código ou o fluxo de desenvolvimento do projeto. Não devemos deixar decisões importantes existir somente da forma de comentários de Pull Request, uma vez que outras pessoas podem achar difícil buscar por PRs antigos e achar as causas de uma implementação ou design existente.
* Se os objetivos ou motivações do Pull Request são estão claras para você, peça à pessoa que abriu o Pull Request uma descrição melhor e explicações. Lembre-se que Pull Requests não são somente sobre adicionar código mas também adicionar conhecimento de negócios.
* Embora os commits em um Pull Request sejam mergeados, eles podem ser significativos por si só. Comente sobre mensagens de commit melhores e aponte para [documentação relevante](#git) quando necessário.
* Aprecie a qualidade do trabalho da sua equipe <3.
* Tente usar ao máximo a interface do GitHub e o [GitHub Flavored Markdown](#github-flavored-markdown) quando revisar código: marque pedaços de código, faça referências entre commits e outras issues e chame outras pessoas para ajudar na revisão. Apenas evite comentar no PR diretamente ao invés dos diffs, uma vez que polui a página do PR e esses comentários não serão escondidos quando as linhas relacionadas mudarem ou forem corrigidas por um novo commit.
* Revisar Pull Requests pode ser mais importante que abrir o seu próprio. Você deverá ter o hábito de ajudar sua equipe a lançar ótimas features e código de qualidade, e vice-versa. Revisar Pull Requests não é algo que deve ser feito no seu tempo livre - deve ser parte do seu fluxo diário. E lembre-se que dedicar sua atenção e tempo para revisar o trabalho de outra pessoa é a maior prova que você se importa com o trabalho dela.

### Seu Pull Request Revisado

Mais cedo ou mais tarde você vai abrir um Pull Request. É parte do seu fluxo de trabalho, como já mencionamos. Toda a equipe vai ter a oportunidade de revisar suas mudanças. Discussões serão levantadas, exemplos de código serão mostrados, experiências serão compartilhadas. Tudo é parte do processo de revisão.

Quando estiver passando por uma, por favor considere os seguintes itens:

* Crie um Pull Request bem explicado. Quando estiver escrevendo, finja que está descrevendo as mudanças para uma pessoa que não tem o contexto do problema.
* Responda os questionamentos e comentários que virão.
* Não leve para o lado pessoal. Ninguém está querendo que você se sinta mal ou que você fique desconfortável na equipe de desenvolvimento.
* Seja sempre humilde. Aprenda com seus erros.
* Entenda as outras alternativas antes de escolher alguma delas ou manter a solução que você propôs. Se você não entendeu completamente porquê alguém pediu alguma mudança, peça explicações e/ou exemplos.

### Mergeando Pull Requests

Uma vez que tudo estiver revisado, melhorias forem feitas e o código está pronto para ser entregue, é hora de mergear o Pull Request na branch principal. Primeiramente, certifique-se de que a feature branch poderá ser mergeada sem problemas na branch principal. A UI do GitHub facilita bastante isso:

![merge conflict](../images/merge-conflict.png "")

Pull Requests que não podem ser mergeados automaticamente irão causar conflitos de merge, já que ambos têm mudanças conflitantes nos mesmos arquivos. Para resolver isso você pode utilizar a própria interface do GitHub, onde você poderá revisar os conflitos e editar o arquivo com conflito, e depois commitar a correção, ou fazer isso na sua própria máquina.

```
  # baixe as últimas mudanças do repositório origin
  $ git checkout master
  $ git pull
  # volte para a sua feature branch e mergeie a main branch nela.
  $ git merge master
  # Resolva os conflitos
  $ git commit
```

Uma vez que você commitou o merge e fez push da feature branch você verá que o GitHub vai poder mergear seu Pull Request automaticament:

![merge conflict](../images/mergeable.png "")

Agora que o merge irá funcionar, você pode apertar aquele botão verde 'Squash and merge' (prefira sempre o squash) e a feature branch será mergeada na main branch! Depois disso, não se esqueça de apagar a feature branch já que ela não será usada mais - você pode fazer isso logo depois do merge pela interface do GitHub.
