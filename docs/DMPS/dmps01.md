# DMPS - TUTORIAL 01

Elaborado por:
<br/>
Jonathan Cardoso Lopes Domingos
<br/>
02/01/2020

Neste exemplo iremos importar um CSV via http. O csv pertence ao site do <button onclick="window.open('http://dados.turismo.gov.br/');">Ministério do Turismo</button>. Este csv contém entre outras, as informações
sobre ementa parlamentar destinado a alguns municípios brasileiros. 

## Importando CSV via http.

OBS: Para esta série de atividades estarei utilizando o DMPS em uma máquina virtual na AWS.

> Tela inicial do login do DMPS


-------------------------

![Screenshot](../../img/dmps1/01.jpg)

------------------------


> Plataforma de Trabalho do DMPS

-------------------------

![Screenshot](../../img/dmps1/02.jpg)

------------------------


> Iniciando um novo Job


-------------------------

![Screenshot](../../img/dmps1/03.jpg)

------------------------


> Adicionar nome e descrissão

-------------------------

![Screenshot](../../img/dmps1/04.jpg)

------------------------

> No lado esquerdo temos os Jobs steps, que são estapas do nosso fluxo de decião. 

-------------------------

![Screenshot](../../img/dmps1/05.jpg)

------------------------

## Job Step: http-inbound


> Para importar um CSV de um link HTTP usaremos o Job step **http-inbound**. Basta segurar e arrastar o job para o centro da mesa de trabalho. 


-------------------------

![Screenshot](../../img/dmps1/06.jpg)

------------------------



> Dando um duplo clique sobre o job step, voce pode comecar a configura-lo. Siga o passo das imagens abaixo. 

-------------------------

![Screenshot](../../img/dmps1/07.jpg)

------------------------

OBS: O DMPS obriga você a escolher uma autenticação, mesmo que o link seja livre. 
No nosso caso usaremos um link livre. Logo em Username e Password você poderá colocar qualquer caractere. 
Eu optei por colocar admin no Username e admin no Password. 


link para o arquivo csv:  

> http://dados.turismo.gov.br/images/csv/emendas/2017-emendas.csv


-------------------------

![Screenshot](../../img/dmps1/08.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/09.jpg)

------------------------


> Antes de colocar nosso próximo job step, observe o nosso dataset:

-------------------------

![Screenshot](../../img/dmps1/01tab.jpg)

------------------------


> Nossa tabela apresenta algumas inconsistencias nos dados que, na medida que avançaremos com
os tutoriais, iremos corrigir. 

## Job Step: csv-unpack

> Este job faz um "reconhecimento" de uma linha do nosso dataset. Assim podermos trabalhar com índices. 


-------------------------

![Screenshot](../../img/dmps1/10.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/11.jpg)

------------------------


-------------------------

![Screenshot](../../img/dmps1/11Ver.jpg)

------------------------


## Job Step: csv-normalization

> Este job "diz" quais coluna(dados) iremos utilizar em nosso fluxo. 

-------------------------

![Screenshot](../../img/dmps1/12.jpg)

------------------------

OBS: Sempre ver qual é o delimitador do seu CSV.

-------------------------

![Screenshot](../../img/dmps1/13.jpg)

------------------------


> Pegando os dados da coluna 0 (NºConvênio) do nosso dataset e atribuindo o nome de numeroConvenio.
Neste caso estamos dizendo para o nosso fluxo utilizar a coluna zero do nosso dataset, porém ela recebera, dentro do DMPS, o nome de numeroConvenio.

-------------------------

![Screenshot](../../img/dmps1/14.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/15.jpg)

------------------------

> Como vamos trabalhar com mais dados do nosso csv, iremos adicionar quantas iterações necessárias. Cada iteração corresponde a uma coluna que iremos trabalhar. 
Para este Job iremos utilizar as seguintes colunas com os seguintes nomes:

iterations:

- 0 = numeroConvenio
- 1 = modalidade
- 2 = uf 
- 3 = local
- 4 = valorGlobal

-------------------------

![Screenshot](../../img/dmps1/16.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/17.jpg)

------------------------


> Lembre-se de salvar seu progresso com frequência:

-------------------------

![Screenshot](../../img/dmps1/18.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/19.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/20.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/21.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/22.jpg)

------------------------


> Observe que no exemplo a seguir, o valorGlobal receberá o tipo de string. 
Isso acontece por que a notação da coluna Valor Global está com um ponto 
como separador do número (295.500). Neste caso teremos que tratar este dado (o que faremos mais
a diante) para que ele se torne um número inteiro. 
Se você tentar converter sem tratar o DMPS irá mante-lo como string. Ele não 
irá transformar o arquivo em Float pois tem dados que possuem dois pontos (1.239.346).

-------------------------

![Screenshot](../../img/dmps1/23.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/24.jpg)

------------------------

## Job Step: Script 

> Neste job step iremos tratar o problema com os dados valorGlobal. Iremos retirar o ponto e transformar 
o tipo de string para integer. 

-------------------------

![Screenshot](../../img/dmps1/25.jpg)

------------------------


> Você pode escolher entre Python e JavaScrip, recomendo utilizar o Python, 
reza a lenda que ele é infinitas vezes melhor que JS. 

-------------------------

![Screenshot](../../img/dmps1/26.jpg)

------------------------


> Selecione a variavel que iremos tratar.

-------------------------

![Screenshot](../../img/dmps1/27.jpg)

------------------------


> Nomeie uma nova variavel de saída. 
Neste caso, a variável valorGlobal do tipo 
string ira sair como novoValorGlobal do tipo
integer. 

-------------------------

![Screenshot](../../img/dmps1/28.jpg)

------------------------


> Criando um código python para retirar as inconsistencias dos dados. 

-------------------------

![Screenshot](../../img/dmps1/29.jpg)

------------------------


> Lembre-se (SALVAR)

-------------------------

![Screenshot](../../img/dmps1/30.jpg)

------------------------

## Job Step: Visualization-Store

> Agora iremos colocar um job step que permite visualizar os
resultados do nosso processo de stream de dados. 

-------------------------

![Screenshot](../../img/dmps1/31.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/32.jpg)

------------------------


## Job Step: Visualization-Store (Erro)

> Iremos adicionar outro visualization-store para as saídas de erros. 
Todo job que possui códigos está sujeito a uma série de erros, logo
a visualization de erro nos permite ter um log de erros. 

-------------------------

![Screenshot](../../img/dmps1/33.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/34.jpg)

------------------------

> Antes de testar nosso job, iremos fazer um filtro das variáveis que
queremos que siga o nosso fluxo. 

> Dê um duplo clique no fluxo (SHUFFLE) que está entre tratamentoDados e resultados
e desmarque as seguintes opções.  

-------------------------

![Screenshot](../../img/dmps1/37.jpg)

------------------------

## Testando o Fluxo:

> Após todo o processo de construção do fluxo iremos testar. 
Clicar em salvar, verificar o código e por fim clicar em enviar. 

-------------------------

![Screenshot](../../img/dmps1/35.jpg)

------------------------


> Após enviar, você poderá verificar que o seu job estará em situação de 
configurado. Agora bastar rodar o Job e esperar que esteja tudo pronto. 

-------------------------

![Screenshot](../../img/dmps1/36.jpg)

------------------------


> Algumas informações podem indicar que seu job está funcionando. Observe as imagens a seguir:

-------------------------

![Screenshot](../../img/dmps1/38.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/39.jpg)

------------------------


## Visualizando Resultados

> Vá na aba visualization e clique em jobs

-------------------------

![Screenshot](../../img/dmps1/40.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/41.jpg)

------------------------


> Selecione o nome do seu Job

-------------------------

![Screenshot](../../img/dmps1/42.jpg)

------------------------


> Os resultados das suas variáveis irão aparecer.

-------------------------

![Screenshot](../../img/dmps1/43.jpg)

------------------------


> Podemos observar que o novoValorGlobal foi alterado para inteiro. Podemos observar, também, que um valor não está correto.
A variável local está recebendo o valor da coluna Valor Global do nosso csv. 

-------------------------

![Screenshot](../../img/dmps1/44.jpg)

------------------------


## Corrigindo o ERRO


> Para corrigir o erro devemos voltar ao job step que pega as colunas do csv. 
Mas para isso devemos parar o nosso job. 

-------------------------

![Screenshot](../../img/dmps1/45.jpg)

------------------------


> Ir em configure job

-------------------------

![Screenshot](../../img/dmps1/46.jpg)

------------------------

> Dar um duplo clique no job estrairColunas e procurar a iteration que está com problema. 
Neste caso, a iteration 4. Você deverá mudar o fild position para 3. 

-------------------------

![Screenshot](../../img/dmps1/47.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/48.jpg)

------------------------

> Por que isso ocorre?

Observe a imagem a seguir:

-------------------------

![Screenshot](../../img/dmps1/49.jpg)

------------------------


A nossa iteration 4 é a variavél local e no nosso csv a variável 
local está com 3. Isso ocorre por que no csv a primeira coluna é 
a coluna 0 e as iterações começam do 1. 
Após a alteração devemos salvar. Para que as alterações sejam de 
fato visualizada no nosso visualisation job devemos deletar o cash. 
Ir na aba visualization e clicar em jobs. Ir na opção **stores**

-------------------------

![Screenshot](../../img/dmps1/50.jpg)

------------------------

> Em stores clique em atualizar, digite o nome do seu job, clique nos três pontinhos e por fim  deletar. 

-------------------------

![Screenshot](../../img/dmps1/51.jpg)

------------------------

> Após deletar o cash do seu job vá na aba JOBS, clique em All, 
digite o nome do seu job e clique sobre ele. 

-------------------------

![Screenshot](../../img/dmps1/52.jpg)

------------------------

-------------------------

![Screenshot](../../img/dmps1/53.jpg)

------------------------

> Agora basta ir em rodar. 

-------------------------

![Screenshot](../../img/dmps1/54.jpg)

------------------------

> Se tudo deu certo, seu job apresentará os comportamentos normais. 
Como já visualizado anteriormente. 

-------------------------

![Screenshot](../../img/dmps1/55.jpg)

------------------------

> Agora basta ir em visualization - jobs - Discover e selecionar o seu job.
Podemos observar que a variavel local está corrigida. Agora ela apresenta
o nome do município.  
