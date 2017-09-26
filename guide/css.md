# CSS/SCSS #

## Estilo ##

* Deixe um espaço em branco depois de nomes de propriedade (como ```color: #000```) e antes de abrir chaves (como em  ```.selector {```);
* Escreva cores em hexadecimal usando letras minúsculas;
* Escreve novos seletores usando ```-``` como separador de palavras em vez de ```_``` (```section-title``` em vez de ```section_title```);

## Organização de propriedades ##

Tente organizar as propriedades em grupos de funcionalidades relacionados (como os a seguir), e ordene deste modo:

+ Diretivas específicas de pré-processadores, como ```@extends``` ou ```@include```;
+ ```position``` e propriedades relacionadas como ```top```, ```right```, ```z-index``` e afins;
+ ```display``` e propriedades relacionadas ao box-model: ```height```, ```width```, ```padding```, ```margin```, ```box-sizing```, ```visibility```, etc;
+ Definições de fonte (```font```), texto (```text```) (```font-family``` e companhia, ```line-height```, ```text-decoration```) ou cor (```color```);
+ Propriedades relacionadas a ```background``` e ```border```;
+ Propriedades adicionais do CSSS3 como ```box-shadow```, ```transform``` e afins.

Estas regras de agrupamento devem ser suficientes para a maioria do CSS que você vai ver no dia-a-dia.

### O resto ###

No caso de definições complexas e de listas longas de propriedades, considere dividir grupos de estilos relacionados em seletores diferentes e aplicar múltiplas classes ao mesmo elemento.

## Formatação ##

* Você pode separar vários seletores quebrando a linha para melhorar a legibilidade de um conjunto complexo de seletores;

```html
  input[type='submit'],
  input[type='reset'],
  input[type='button'] {
    /* ... */
  }
```

* Se o seletor tiver uma única propriedade você pode escrever em uma linha só:

```.selector { font-weight: bold; }```


## Documentação ##

TODO: não temos documentação definida

## Selector Specificity ##

TODO: notas sobre especificidade

Por enquanto, regra geral é evitar `important!` a todo custo ;)

## Prefixos de browser ##

Caso use prefixos de browser em propriedades e funções, não se esqueça de conferir a compatibilidade no [Can I use…](http://caniuse.com/) para ter certeza que vai funcionar e quais prefixos você precisa. Muitas propriedades de CSS3 não precisam de prefixos em vários browsers, como ```border-radius``` e ```box-shadow```. Se não tiver tanta sorte, coloque as propriedades prefixadas antes da versão não prefixada.

Ou use pré-processadores (ver abaixo).

```css
 .button:hover {
    -moz-transform: background-position .2s ease;
    -ms-transform: background-position .2s ease;
    -o-transform: background-position .2s ease;
    -webkit-transform: background-position .2s ease;
    transform: background-position .2s ease;
  }
```

## Pré-processadores ##

Pré-processadores como [Sass](http://sass-lang.com/), [LESS](http://lesscss.org/) or [Stylus](http://learnboost.github.io/stylus/) são úteis para lidar com um conjunto grande de stylesheets e devemos ter atenção a alguns detalhes para não fazer mau uso dessas ferramentas.

Quando usar variáveis, defina-as com *screaming snake case* para facilitar a busca delas no código. É mais fácil achar ```$FONT_SIZE``` em vez de ```$font-size```;
Use comentários específicos da linguagem como ```//``` em vez do clássico ```/* */``` do CSS. Eles vão funcionar melhor com *syntax highlighters* e sempre serão ignorados quando compilar seus *stylesheets*;
Não abuse do aninhamento - o seletor aninhado é um bom jeito de reduzir a duplicação de seletores pais mas compromete a legibilidade do seu código. Então, tente manter o aninhamento em 2 níveis e mantenha os blocos com no máximo 40/50 linhas, para que eles possam caber em uma tela só no seu editor.

## Organização ##

Cada projeto pode ter sua organização específica.

TODO: listar os tipos mais comuns.

## Referências ##

Partes deste guia foram baseados em vários recursos na Internet:

* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [GitHub CSS Styleguide](https://github.com/styleguide/css)
* [CSS-Tricks Sass Style Guide](http://css-tricks.com/sass-style-guide/)
* [Mark Otto Code guide](https://github.com/mdo/code-guide)
