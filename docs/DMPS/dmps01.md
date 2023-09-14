# DMPS - TUTORIAL 01

Elaborado por:
<br/>
Jonathan Cardoso Lopes Domingos
<br/>
02/01/2020

Neste exemplo iremos importar um CSV via http. O csv pertence ao site do <button onclick="window.open('http://dados.turismo.gov.br/');">Ministério do Turismo</button>. Este csv contém, dentre outras, as informações
sobre emendas parlamentares destinadas a alguns municípios brasileiros. 

## Importando CSV via http.

Obs: para esta série de atividades, estarei utilizando o DMPS em uma máquina virtual na AWS.

> Tela inicial do login do DMPS


-------------------------

![Screenshot](../img/dmps1/01.jpg)

------------------------


> Plataforma de Trabalho do DMPS

-------------------------

![Screenshot](../img/dmps1/02.jpg)

------------------------


> Iniciando um novo Job


-------------------------

![Screenshot](../img/dmps1/03.jpg)

------------------------


> Adicionar nome e descrição

-------------------------

![Screenshot](../img/dmps1/04.jpg)

------------------------

> No lado esquerdo temos os job steps, que são estapas do nosso fluxo de decisão. 

-------------------------

![Screenshot](../img/dmps1/05.jpg)

------------------------

## Job Step: http-inbound


> Para importar um CSV de um link HTTP usaremos o job step **http-inbound**. Basta segurar e arrastar o job para o centro da mesa de trabalho. 


-------------------------

![Screenshot](../img/dmps1/06.jpg)

------------------------



> Dando um duplo clique sobre o job step, você pode começar a configurá-lo. Siga o passo das imagens abaixo. 

-------------------------

![Screenshot](../img/dmps1/07.jpg)

------------------------

Obs: O DMPS obriga você a escolher uma autenticação, mesmo que o link seja livre. 
No nosso caso usaremos um link livre. Logo em Username e Password você poderá colocar qualquer caractere. 
Eu optei por colocar admin no Username e admin no Password. 


Link para o arquivo csv:  

> http://dados.turismo.gov.br/images/csv/emendas/2017-emendas.csv


-------------------------

![Screenshot](../img/dmps1/08.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/09.jpg)

------------------------


> Antes de colocar nosso próximo job step, observe o nosso dataset:

-------------------------

![Screenshot](../img/dmps1/01tab.jpg)

------------------------


> Nossa tabela apresenta algumas inconsistências nos dados que, à medida que avançamos com
os tutoriais, iremos corrigindo. 

## Job Step: csv-unpack

> Este job faz um "reconhecimento" de uma linha do nosso dataset. Assim podemos trabalhar com índices. 


-------------------------

![Screenshot](../img/dmps1/10.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/11.jpg)

------------------------


-------------------------

![Screenshot](../img/dmps1/11Ver.jpg)

------------------------


## Job Step: csv-normalization

> Este job nos mostra quais coluna(dados) iremos utilizar em nosso fluxo. 

-------------------------

![Screenshot](../img/dmps1/12.jpg)

------------------------

Obs: sempre ver qual é o delimitador do seu CSV.

-------------------------

![Screenshot](../img/dmps1/13.jpg)

------------------------


> Pegando os dados da coluna 0 (Nº Convênio) do nosso dataset e atribuindo o nome de numeroConvenio.
Neste caso, estamos dizendo para o nosso fluxo utilizar a coluna zero do nosso dataset, porém ela receberá dentro do DMPS o nome de numeroConvenio.

-------------------------

![Screenshot](../img/dmps1/14.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/15.jpg)

------------------------

> Como vamos trabalhar com mais dados do nosso csv, iremos adicionar quantas iterações forem necessárias. Cada iteração corresponde a uma coluna que iremos trabalhar. 
Para este job, iremos utilizar as seguintes colunas com os seguintes nomes:

iterations:

- 0 = numeroConvenio
- 1 = modalidade
- 2 = uf 
- 3 = local
- 4 = valorGlobal

-------------------------

![Screenshot](../img/dmps1/16.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/17.jpg)

------------------------


> Lembre-se de salvar seu progresso com frequência:

-------------------------

![Screenshot](../img/dmps1/18.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/19.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/20.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/21.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/22.jpg)

------------------------


> Observe que no exemplo a seguir, o valorGlobal receberá o tipo de string. 
Isso acontece por que a notação da coluna Valor Global está com um ponto 
como separador do número (295.500). Neste caso, teremos que tratar este dado (o que faremos mais
adiante) para que ele se torne um número inteiro. 
Se você tentar converter sem tratar, o DMPS irá mantê-lo como string. Ele não 
irá transformar o arquivo em Float pois tem dados que possuem dois pontos (1.239.346).

-------------------------

![Screenshot](../img/dmps1/23.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/24.jpg)

------------------------

## Job Step: Script 

> Neste job step iremos tratar o problema com os dados valorGlobal. Iremos retirar o ponto e transformar 
o tipo de string para integer. 

-------------------------

![Screenshot](../img/dmps1/25.jpg)

------------------------


> Você pode escolher entre Python e JavaScript. Eu recomendo utilizar o Python, 
reza a lenda que ele é infinitas vezes melhor que JS. 

-------------------------

![Screenshot](../img/dmps1/26.jpg)

------------------------


> Selecione a variável que iremos tratar.

-------------------------

![Screenshot](../img/dmps1/27.jpg)

------------------------


> Nomeie uma nova variável de saída. 
Neste caso, a variável valorGlobal do tipo 
string irá sair como novoValorGlobal do tipo
integer. 

-------------------------

![Screenshot](../img/dmps1/28.jpg)

------------------------


> Criando um código python para retirar as inconsistências dos dados. 

-------------------------

![Screenshot](../img/dmps1/29.jpg)

------------------------


> Lembre-se: SALVAR

-------------------------

![Screenshot](../img/dmps1/30.jpg)

------------------------

## Job Step: Visualization-Store

> Agora iremos colocar um job step que permite visualizar os
resultados do nosso processo de streaming de dados. 

-------------------------

![Screenshot](../img/dmps1/31.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/32.jpg)

------------------------


## Job Step: Visualization-Store (Erro)

> Iremos adicionar outro visualization-store para as saídas de erros. 
Todo job que possui códigos está sujeito a uma série de erros, logo
a visualization de erro nos permite ter um log de erros. 

-------------------------

![Screenshot](../img/dmps1/33.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/34.jpg)

------------------------

> Antes de testar nosso job, iremos fazer um filtro das variáveis que
queremos que siga o nosso fluxo. 

> Dê um duplo clique no fluxo (SHUFFLE) que está entre tratamentoDados e resultados
e desmarque as seguintes opções.  

-------------------------

![Screenshot](../img/dmps1/37.jpg)

------------------------

## Testando o Fluxo:

> Após todo o processo de construção do fluxo, faremos um teste: 
clicar em salvar, verificar o código e por fim clicar em enviar. 

-------------------------

![Screenshot](../img/dmps1/35.jpg)

------------------------


> Após enviar, você poderá verificar que o seu job estará em situação de 
configurado. Agora basta rodar o job e esperar que esteja tudo pronto. 

-------------------------

![Screenshot](../img/dmps1/36.jpg)

------------------------


> Algumas informações podem indicar que seu job está funcionando. Observe as imagens a seguir:

-------------------------

![Screenshot](../img/dmps1/38.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/39.jpg)

------------------------


## Visualizando Resultados

> Vá na aba visualization e clique em jobs

-------------------------

![Screenshot](../img/dmps1/40.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/41.jpg)

------------------------


> Selecione o nome do seu Job

-------------------------

![Screenshot](../img/dmps1/42.jpg)

------------------------


> Os resultados das suas variáveis irão aparecer.

-------------------------

![Screenshot](../img/dmps1/43.jpg)

------------------------


> Podemos observar que o novoValorGlobal foi alterado para inteiro. Podemos observar, também, que um valor não está correto.
A variável local está recebendo o valor da coluna Valor Global do nosso csv. 

-------------------------

![Screenshot](../img/dmps1/44.jpg)

------------------------


## Corrigindo o ERRO


> Para corrigir o erro devemos voltar ao job step que pega as colunas do csv. 
Mas para isso devemos parar o nosso job. 

-------------------------

![Screenshot](../img/dmps1/45.jpg)

------------------------


> Ir em configure job

-------------------------

![Screenshot](../img/dmps1/46.jpg)

------------------------

> Dar um duplo clique no job extrairColunas e procurar a iteration que está com problema. 
Neste caso, é a iteration 4. Você deverá mudar o field position para 3. 

-------------------------

![Screenshot](../img/dmps1/47.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/48.jpg)

------------------------

> Por que isso ocorre?

Observe a imagem a seguir:

-------------------------

![Screenshot](../img/dmps1/49.jpg)

------------------------


A nossa iteration 4 é a variavél local e no nosso csv a variável 
local está com 3. Isso ocorre por que no csv a primeira coluna é 
a coluna 0 e as iterações começam do 1. 
Após a alteração, devemos salvar o que foi feito. Para que as alterações sejam de 
fato visualizadas no nosso visualization job, devemos deletar o cash. 
Ir na aba visualization e clicar em jobs. Ir na opção **stores**

-------------------------

![Screenshot](../img/dmps1/50.jpg)

------------------------

> Em stores clique em atualizar, digite o nome do seu job, clique nos três pontinhos e, por fim, clique em deletar. 

-------------------------

![Screenshot](../img/dmps1/51.jpg)

------------------------

> Após deletar o cash do seu job, vá na aba JOBS, clique em All, 
digite o nome do seu job e clique sobre ele. 

-------------------------

![Screenshot](../img/dmps1/52.jpg)

------------------------

-------------------------

![Screenshot](../img/dmps1/53.jpg)

------------------------

> Agora basta ir em rodar. 

-------------------------

![Screenshot](../img/dmps1/54.jpg)

------------------------

> Se tudo deu certo, seu job apresentará os comportamentos normais, como já visualizado anteriormente. 

-------------------------

![Screenshot](../img/dmps1/55.jpg)

------------------------

> Agora basta ir em visualization - jobs - discover e selecionar o seu job.
Podemos observar que a variável local está corrigida. Agora ela apresenta
o nome do município.  
