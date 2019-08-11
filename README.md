# tcc_econ_esag

Modelo de TCC para o curso de Ciências Econômicas na UDESC/Esag utilizando RMarkdown para escrever a monografia em conjunto com o código em R necessário para as aplicações.

Este modelo faz uso dos pacotes R, `tinytex` e  `bookdown`, além daqueles que em geral já vêm instalados com a interface RStudio (altamente sugerida) como o `knitr` e `rmarkdown`.

As melhores fontes de referência para a utilização do `bookdown` para escrever documentos é seu próprio livro, intitulado [bookdown: Authoring Books and Technical Documents with R Markdown](https://bookdown.org/yihui/bookdown/) e o guia [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/). Além destes, um conhecimento introdutório de Latex é sugerido.

Maiores detalhes de como utilizar o Latex podem ser encontrados em sua documentação oficial, [The Latex Project](https://www.latex-project.org/help/documentation/) e para os detalhes específicos da classe ABNTex2, que implementa o padrão ABNT, o site oficial é [https://www.abntex.net.br/](https://www.abntex.net.br/).

# Instalação

Para a "instalação" do repositório é possível fazer um _fork_ dele, copiando-o para sua própria conta no Github. Ou então copiar todos os documentos zipados e descompactar numa pasta de seu computador local, o link para baixar o zip é: [https://github.com/rfbressan/tcc_econ_esag/archive/master.zip](https://github.com/rfbressan/tcc_econ_esag/archive/master.zip) que também pode ser encontrado no botão verde acima "Clone or Download", seta para baixo e então "Download ZIP". 

# Primeira coisa

Após "instalar" o repositório, abra o projeto através do R (sugiro o RStudio, melhor ainda se for via rstudio.cloud) e proceda da seguinte maneira:

- Instalar o pacote R `tinytex` com o comando `install.packages("tinytex")`
- Instalar o pacote Latex `tinytex` usando o próprio pacote do R. No console digite `tinytex::install_tinytex()`
- Instalar os pacotes Latex `babel-portuges` e `babel-english`. No console digite `tinytex::tlmgr_install(c("babel-portuges", "babel-english"))`
- Atualizar o pacote Latex `biber` que, por algum motivo desconhecido vem desatualizado em relação ao `biblatex`. No console digite `tinytex::tlmgr_install("biber")`

# Customizando com Latex

O formato RMarkdown nada mais é que uma espécie de híbrido entre outros formatos conhecidos de texto e código em R (e até outras linguagens). Entre estes formatos de texto estão o markdown puro e o Latex. Quando o arquivo final será em formato `pdf`, o knitr transforma o arquivo `.Rmd` interpretando os códigos, em formato markdown (extensão .md) e passa este arquivo ao `pandoc`. Este por sua vez, transforma o arquivo .md para o formato do Latex (extensão .tex) que finalmente será compilado para o seu destino final, arquivo pdf.

Como em um passo intermediário é criado um arquivo do Latex, é possível incluir, tanto diretamente no texto RMarkdown, comandos Latex (e.g. é possível abrir um ambiente matemático com \begin{equation}), como via arquivos `.tex` a serem incluídos em partes específicas do arquivo intermediário que será compilado posteriormente. Esta é a função da diretiva YAML `includes:`.

## O arquivo `preamble.tex`

A diretiva `includes:` aceita como opção a definição `in_header: arquivo.tex`. Esta diretiva faz com que o `arquivo.tex` seja **inserido** no preâmbulo de nosso arquivo Latex principal. Desta forma, no modelo de TCC apresentado, o arquivo `preamble.tex` tem a função de carregar todos os pacotes Latex necessários para a compilação do arquivo pdf final assim como determinar algumas configurações globais do trabalho, como o espaçamento entre linhas e a identação do parágrafo.

O arquivo `preamble.tex` deve ser editado conforme a necessidade do usuário.
 
## O arquivo `beforebody.tex`

Por sua vez, a definição `before_body: beforebody.tex` faz com que o arquivo `beforebody.tex` seja **inserido** antes do corpo de texto. Ou seja, logo após a abertura do bloco \begin{document} mas antes dos capítulos. Este é o arquivo responsável por gerar todos os elementos pré-textuais e portanto, deve ser editado conforme a necessidade do usuário e o padrão exigido por sua instituição de ensino.

# Dados da monografia

Os dados relativos ao título, autor e data da monografia estão no YAML do arquivo `index.Rmd`. Entretanto, o restante dos dados como local, professor orientador, instituição de ensino, etc. se econtram na subpasta `/extras` no arquivo `dados.tex` e podem (devem) ser editadas diretamente neste arquivo.

# Dados pré-textuais

Já os dados pré-textuais do trabalho se encontram na subpasta `/pretextual` em vários arquivos, cada um com uma finalidade específica. Assim, se na sua monografia você deseja incluir uma página contendo agradecimentos, deve primeiramente descomentar no arquivo `beforebody.tex` a linha referente aos agradecimentos, `\include{pretextual/agradecimentos}` e então editar o respectivo arquivo com o seu agradecimento. A mesma lógica segue para a capa, folha de rosto, ficha catalográfica, dedicatória, folha de aprovação, epígrafe e resumos.

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