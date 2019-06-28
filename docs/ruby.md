# Ruby

>O Ruby é simples na aparência, mas muito complexo no interior, tal como o corpo humano - Yukihiro Matsumoto

Ruby é uma linguagem de programação interpretada multiparadigma, de tipagem dinâmica e forte, com gerenciamento de memória automático, originalmente planejada e desenvolvida no Japão em 1995, por Yukihiro "Matz" Matsumoto, para ser usada como linguagem de script. Matz queria uma linguagem de script que fosse mais poderosa do que Perl, e mais orientada a objetos do que Python. Ruby suporta programação funcional, orientada a objetos, imperativa e reflexiva.

**Instalando o Ruby**

Em sistemas Unix como Ubuntu, você pode abrir o Terminal e digitar o comando ​
 
```
apt-get install ruby​
```
Ou pode usar um gerenciador de versão para a instalação como o ​ RVM​. Para isso recomento utilizar o tutorial da própria documentação do ruby <https://www.ruby-lang.org/en/downloads/> ou utilizar a documentação do RMV <https://rvm.io/>. 

#My Ruby Cheat Sheet 

Esta é minha documentação para consulta de comandos em Ruby. Foi elaborada com base em comandos criados por mim e com base em consulta nos seguintes endereços:

https://www.devmedia.com.br/introducao-ao-recursos-basicos-da-linguagem-ruby/31504

https://github.com/albertoleal/prazer--ruby/blob/master/trabalhando-com-strings.mkdn

https://www.ruby-lang.org/pt/documentation/quickstart/


```Ruby
#Shell Interativo
$ irb
```

Exemplo de utilização do comando puts com aspas simples e aspas duplas. 

```Ruby
2.6.3 :002 > puts "def teste\n\tputs teste\nend"
def teste
	puts teste
end
 => nil 
```

```Ruby
2.6.3 :003 > puts 'def teste\n\tputs teste\nend'
def teste\n\tputs teste\nend
 => nil 
```

#STRINGS

```Ruby

#Gerando Strings 

2.6.3 :012 > s1 = "Isso é uma string"
 => "Isso é uma string" 

2.6.3 :013 > s2 = 'Isso, também, é uma string'
 => "Isso, também, é uma string" 

2.6.3 :014 > s3 = %q[Mais uma forma de se criar uma string] 
 => "Mais uma forma de se criar uma string" 

2.6.3 :015 > s4 = %Q[Outra forma de se criar uma string]
 => "Outra forma de se criar uma string" 

#Substituindo Strings

#sub
2.6.3 :031 > str = "Olá, meu nome é Jonathan"
 => "Olá, meu nome é Jonathan" 
2.6.3 :032 > str.sub(/Jonathan/, "Leda")
 => "Olá, meu nome é Leda"

#gsub
2.6.3 :035 > str = "Olá, meu nome é Jonathan, caro amigo Jonathan"
 => "Olá, meu nome é Jonathan, caro amigo Jonathan" 
2.6.3 :036 > str.gsub(/Jonathan/, "Leda")
 => "Olá, meu nome é Leda, caro amigo Leda" 

#Pesquisando Strings

2.6.3 :054 > str = "Hoje o sol não apareceu, é o fim!"
 => "Hoje o sol não apareceu, é o fim!" 
2.6.3 :056 > str[7,3]
 => "sol"

#Buscando a posição da String

2.6.3 :057 > str = "Hoje o Sol não Apareceu, é o fim!"
 => "Hoje o Sol não Apareceu, é o fim!" 
2.6.3 :058 > str.index(/apareceu/i)
 => 15 
#o i foi usado para tornar a busca não case-sensitive

#Retornado Arrays de strings

2.6.3 :059 > str = "Hoje a noite não tem luar"
 => "Hoje a noite não tem luar" 

2.6.3 :060 > str.scan(/\w/)
 => ["H", "o", "j", "e", "a", "n", "o", "i", "t", "e", "n", "o", "t", "e", "m", "l", "u", "a", "r"] 

2.6.3 :061 > str.scan(/\w+/)
 => ["Hoje", "a", "noite", "n", "o", "tem", "luar"] 

2.6.3 :080 > str.split
 => ["Hoje", "a", "noite", "não", "tem", "luar"] 

#Espaços em Strings
2.6.3 :097 > str = 'Jonathan Cardoso'
 => "Jonathan Cardoso" 
2.6.3 :098 > str.ljust(20)
 => "Jonathan Cardoso    " 
2.6.3 :099 > str.rjust(20)
 => "    Jonathan Cardoso" 
2.6.3 :100 > str.center(20)
 => "  Jonathan Cardoso  " 


#Métodos em Strings

2.6.3 :004 >'jonathan'.upcase
 => "JONATHAN"

2.6.3 :005 > 'JoNaThan'.capitalize
 => "Jonathan" 

2.6.3 :006 > 'JONATHAN'.downcase
 => "jonathan"

2.6.3 :104 > 'JoNaThaN'.swapcase
 => "jOnAtHAn"

2.6.3 :007 > 'JONATHAN'.length  #'JONATHAN'.size
 => 8 

2.6.3 :115 > 'JJooNnaTTthan'.squeeze
 => "JoNnaTthan" #Remove caracters duplicados

2.6.3 :128 > 'Jonathan'.reverse
 => "nahtanoJ"

2.6.3 :138 > 'Jonathan Cardoso'.split("").reverse.join("")
 => "osodraC nahtanoJ"

2.6.3 :171 > puts 'Jonathan'.count('a')
 => 2
```

#Interpolação

Nos exemplos abaixo foi utilizado o construtor #{}, que serve para substituições de varáveis. Essa técnica é conhecida como interpolation. Note que em ambos os exemplos foram utilizados as aspas duplas. 

```Ruby
2.6.3 :013 > "Agora é #{Time.now}"
 => "Agora é 2019-06-27 19:24:27 -0300" 
```

```Ruby
2.6.3 :015 > nome = 'jonathan'
 => "jonathan"

2.6.3 :043 > "Meu nome é:  #{nome}"
 => "Meu nome é:  jonathan" 
```

#To_i e To_f

```Ruby
2.6.3 :152 > 'Jonathan10'.to_f
 => 0.0 
2.6.3 :153 > '105Jonathan'.to_i
 => 105 
2.6.3 :154 > '105Jonathan'.to_f
 => 105.0 

```

#Array

```Ruby
# array vazio
var1 = []

# um array armazenando três strings
var1 = ['casa', 'cavalo', 15]
var1[0] #retorna casa
var1[2] #retorno 15

# Tipos de objetos no Array, inclusive array
var2 = [80.5, 'lua', 10 ,[true, false]]
var2[3][1] #retorno false

#Adicionar objetos
var2[4] = 'sol'
var2 << 'casa'
var2 + ['vento']

#métodos da classe array
var3 = [15, 24, 189, 1]
var3.sort #embaralha a matriz
var3.lengthm #retorno 4
var3.first #retorno 15
var3.last #retorno 1

# o método each
#(do end): é um bloco de código. A variável lang se refere a cada item no array a medida que ele é iterado no loop
alimento = ['chocolate', 'bolo', 'sorvete']

alimento.each do |lang|
   puts 'Eu amo ' + lang + '!'
   puts 'voce nao?'
end
'''
Eu amo chocolate!
voce nao?
Eu amo bolo!
voce nao?
Eu amo sorvete!
voce nao?
 => ["chocolate", "bolo", "sorvete"]

'''
 
# apaga uma entrada no meio e desloca o restante da entradas

alimento.delete('bolo')
alimento.each do |lang|
    puts 'Eu amo ' + lang + '!'
    puts 'voce nao?'
end
'''
Eu amo chocolate!
voce nao?
Eu amo sorvete!
voce nao?
 => ["chocolate", "sorvete"] 
'''

```

#Hash


```Ruby
meu_hash = {nome: "Jonathan", idade: 31, curso: "Mat"}

meu_hash[:nome] #"Jonathan"
meu_hash.first  #[:nome, "Jonathan"]
meu_hash.keys   #[:nome, :idade, :curso]
meu_hash [:curso] = "Geo" #substitui Mat

```

#Função


```Ruby
def divisao (primeiro_numero, segundo_numero)
    if segundo_numero == 0 
        return 'Não é possível dividir por zero'
    else 
        return primeiro_numero / segundo_numero
    end
end

divisao(10, 5)

```
#Blocos e Iterações

```Ruby

2.6.3 :103 > 3.times { puts "Olá!" }
Olá!
Olá!
Olá!
 => 3 

     
2.6.3 :104 > :063 > numeros = [1, 2, 3] 
2.6.3 :105 > :065 > numeros.each {|numero| puts numero} 
1 
2 
3 
=> [1, 2, 3] 
   
 
2.6.3 :106 > numeros = [1, 2, 3] 
2.6.3 :107 > numeros.each do |numero| 
2.6.3 :108 >     puts numero 
2.6.3 :109?>   end 
1 
2 
3 
 => [1, 2, 3]  


2.6.3 :110  > numeros = [1, 2, 3] 
2.6.3 :111  > numeros.each_with_index do |numero, index| 
2.6.3 :112 >     puts "Valor: #{numero}, Índice: #{index}"  
2.6.3 :113?>   end 
Valor: 1, Índice: 0 
Valor: 2, Índice: 1 
Valor: 3, Índice: 2 
 => [1, 2, 3]


```

#Classe



```Ruby
01 class Jogador
02  attr_acessor :primeiro_nome, :ultimo_nome, :numero
03
04  def initialize (prim_nome, ult_nome, numero)
05   @primeiro_nome = prim_nome
06   @ultimo_nome = ult_nome
07   @numero = numero
08  end
09
10  def nome_completo 
11    “#{ultimo_nome.capitalize}, #{primeiro_nome.capitalize}”
12  end
13
14  def posição
15   while @numero == 0 || @numero < 0
16      puts “Coloque novamente um número possível: “
17      @numero = gets.to_i
18   end
19    if @numero < 6 && @numero <0
20     return “Zaga”
21    elsif @numero >= 6 && @numero <=10
22      return “Meio Campo”
23    else
24      return “Ataque”
25    end
26   end
27  end
28 jogador = jogador .new(gets.chomp, gets.chomp, gets.to_i)
29 p “#{jogador.nome_completo} – Função no(a): #{jogador.posicao}”
```
Ainda em construção...