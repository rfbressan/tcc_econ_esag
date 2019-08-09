# tcc_econ_esag

Modelo de TCC para o curso de Ciências Econômicas na UDESC/Esag utilizando RMarkdown para escrever a monografia em conjunto com o código em R necessário para as aplicações.

Este modelo faz uso dos pacotes R, `tinytex` e  `bookdown`, além daqueles que em geral já vêm instalados com a interface RStudio (altamente sugerida) como o `knitr` e `rmarkdown`.

As melhores fontes de referência para a utilização do `bookdown` para escrever documentos é seu próprio livro, intitulado [bookdown: Authoring Books and Technical Documents with R Markdown](https://bookdown.org/yihui/bookdown/) e o guia de [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/). Além destes, um conhecimento introdutório de Latex é sugerido.

# Primeira coisa

- Instalar o pacote R `tinytex` com o comando `install.packages("tinytex")`
- Instalar o pacote Latex `tinytex` usando o próprio pacote do R. No console digite `tinytex::install_tinytex()`
- Instalar o pacote Latex `babel-portuges` e `babel-english`. No console digite `tinytex::tlmgr_install(c("babel-portuges", "babel-english"))`

# Editando os capítulos

A introdução do TCC deve ser escrita no arquivo index.Rmd, que é o arquivo principal do documento, onde constam também as configurações do mesmo como margens, idioma, fonte, etc.

O restante dos capítulos devem ser escritos em arquivos `.Rmd` separados e nomeados na ordem em que se deseja que apareçam os capítulos no TCC. Sugere-se a adoção do formato `número capítulo-nome capítulo` (e.g. 02-revisao.Rmd). Todos estes arquivos **devem** começar com um título de primeiro nível em markdown, ou seja, com `# Nome do capítulo`. Atentar para o fato que o manual da UDESC exige que os capítulos sejam todos nomeados em caixa alta.

## Citações

As citações a referências bibliográficas devem ser feitas através dos formatos `@Gatheral2014` ou `(@Gatheral2014)`, onde um arquivo do tipo `.bib` deve existir na raiz do projeto e deve ser indicado na seção YAML de index.Rmd no campo `bibliography`. O modelo utiliza o arquivo library.bib. As entradas no arquivo `.bib` podem ser facilmente encontradas e copiadas do serviço [Google Acadêmico](https://scholar.google.com.br/).

## Referências Cruzadas

Estas podem ser feitas utilizando o comando `\@ref(referência)` criado pelo `bookdown`. Para se criar uma referência deve-se utilizar o comando `(\#ref(referência))` dentro de um ambiente de equação do Latex se for uma equação, ou utilizar o comando `{#referência}` para outras referências criadas pelo usuário, como seções dos capítulos, etc. Para maiores detalhes verificar a documentação sobre [equações](https://bookdown.org/yihui/bookdown/markdown-extensions-by-bookdown.html#equations) e [referêcias cruzadas](https://bookdown.org/yihui/bookdown/cross-references.html)

# Compilando o TCC

O arquivo pdf a ser gerado deve ser compilado com o comando `bookdown::render_book('index.Rmd', 'bookdown::pdf_book')` no console do R. Se estiver usando o RStudio, o que é recomendado, o script `_build.sh` pode ser chamado através do menu `Build/Configure Build Tools...` e então no painel `Build` o botão `Build All` estará disponível.

O TCC será compilado para uma pasta chamada `_book` que conterá o arquivo `tcc.pdf`. A primeira página gerada deve ser **descartada**. As demais serão o TCC no formato exigido pelo [Manual de Trabalhos Acadêmicos da Udesc](https://udesc.br/arquivos/udesc/documentos/Manual_2017___atualizado_15351282816152_4769.pdf)