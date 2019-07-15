# Ruby

>O Ruby é simples na aparência, mas muito complexo no interior, tal como o corpo humano - Yukihiro Matsumoto

Ruby é uma linguagem de programação interpretada multiparadigma, de tipagem dinâmica e forte, com gerenciamento de memória automático, originalmente planejada e desenvolvida no Japão em 1995, por Yukihiro "Matz" Matsumoto, para ser usada como linguagem de script. Matz queria uma linguagem de script que fosse mais poderosa do que Perl, e mais orientada a objetos do que Python. Ruby suporta programação funcional, orientada a objetos, imperativa e reflexiva.

**Instalando o Ruby**

Em sistemas Unix como Ubuntu, você pode abrir o Terminal e digitar o comando ​
 
```
apt-get install ruby​
```
Ou pode usar um gerenciador de versão para a instalação como o ​ RVM​. Para isso recomento utilizar o tutorial da própria documentação do ruby <https://www.ruby-lang.org/en/downloads/> ou utilizar a documentação do RMV <https://rvm.io/>. 


#GEM

```Ruby
gem install os
gem uninstall os
gem list
```
**Instalando gem com o Bundle**

1. Instalar o Bundle

```Ruby
gem install bundler #(bundler é tipo um estalador de gens)
```

2. Criar um aquivo GemFile sem extenção e colocar a lista de gens que quero.

```
source 'https://rubygems.org'

gem 'os'
gem 'http', '-> 3.3'
```

3. Depois rodar bundle no terminal, na pasta que esta a lista criada.

> $bundle

Este comando ira procurar por uma lista de gem e instala-las.


#Require

```Ruby
require 'os'

def myOS
  if OS.windows?
    "seu sistema é windows"
  elsif OS.linux?
    "seu sistema é linux"
  else
    "não identificamos seu OS"
  end
end

puts "O seu PC possui #{OS.cpu_count} cores, é #{OS.bits} bits e #{myOS}"
```

#My Ruby Cheat Sheet

[Ainda em construção]

Esta é minha documentação para consulta de comandos em Ruby. Foi elaborada com base em comandos criados por mim e com base em consulta nos seguintes endereços:

https://www.devmedia.com.br/introducao-ao-recursos-basicos-da-linguagem-ruby/31504

https://github.com/albertoleal/prazer--ruby/blob/master/trabalhando-com-strings.mkdn

https://www.ruby-lang.org/pt/documentation/quickstart/

http://www.akitaonrails.com/2012/06/29/algumas-dicas-da-linguagem-ruby

https://medium.com/trainingcenter/ruby-101-o-b%C3%A1sico-260e8605962


```Ruby
#Shell Interativo
$ irb
```


#STRINGS

Exemplo de utilização do comando puts com aspas simples e aspas duplas (strings)

```Ruby
In:  puts 'Hoje o sol\n\não apareceu\né o fim!'
Out: Hoje o sol\n\não apareceu\né o fim!
```

```Ruby
In:  puts "Hoje o sol\n\tnão apareceu\né o fim!"
Out: hoje o sol
        não apareceu
     é o fim!
```

```Ruby
#Gerando Strings 

In: s1 = "Isso é uma string"
out: "Isso é uma string" 

In: s2 = 'Isso, também, é uma string'
out: "Isso, também, é uma string" 

In: s3 = %q[Mais uma forma de se criar uma string]
Out: "Mais uma forma de se criar uma string" 

In: s4 = %Q[Outra forma de se criar uma string]
Out: "Outra forma de se criar uma string" 

#Substituindo Strings

#sub
In: str = "Olá, meu nome é Jonathan"
In: str.sub(/Jonathan/, "Leda")
Out: "Olá, meu nome é Leda"

#gsub
In: str = "Olá, meu nome é Jonathan, caro amigo Jonathan"
In: str.gsub(/Jonathan/, "Leda")
Out: "Olá, meu nome é Leda, caro amigo Leda"

#Pesquisando Strings
In: str = "Hoje o sol não apareceu, é o fim!"
In: str[7,3]
Out: "sol"

#Buscando a posição da String
#o i foi usado para tornar a busca não case-sensitive
In: str = "Hoje o Sol não Apareceu, é o fim!"
In: str.index(/apareceu/i)
Out: 15

#Scam
In: str = "Hoje a noite não tem luar"
In: str.scan(/\w/)
Out: ["H", "o", "j", "e", "a", "n", "o", "i", "t", "e", "n", "o", "t", "e", "m", "l", "u", "a", "r"] 

In: str.scan(/\w+/)
Out: ["Hoje", "a", "noite", "n", "o", "tem", "luar"] 

#Split
In: str.split
Out: ["Hoje", "a", "noite", "não", "tem", "luar"] 

#Espaços em Strings
In: str = 'Jonathan Cardoso'
In: str.ljust(20)
Out: "Jonathan Cardoso    "

In :str.rjust(20)
Out:"    Jonathan Cardoso"

In: str.center(20)
Out: "  Jonathan Cardoso  "


#Métodos em Strings
In: 'jonathan'.upcase
Out: "JONATHAN"

In:'JoNaThan'.capitalize
Out: "Jonathan" 

In: 'JONATHAN'.downcase
Out: "jonathan"

In: 'JoNaThaN'.swapcase
Out: "jOnAtHAn"

In: 'JONATHAN'.length  #'JONATHAN'.size
Out: 8 

In: 'JJooNnaTTthan'.squeeze
 => "JoNnaTthan" #Remove caracters duplicados

In: 'Jonathan'.reverse
Out: "nahtanoJ"

In: 'Jonathan Cardoso'.split("").reverse.join("")
Out: "osodraC nahtanoJ"

In: 'Jonathan'.count('a')
Out: 2

In: "I have white space".delete(' ') #deletar os espaços
Out: "Ihavewhitespace"
```

Para converter tipos, devemos usar os métodos to_i, to_f e to_s.

```Ruby
In: "10".to_i   #Transforma em Integer
Out: 10

In: "10.23".to_F   #Transforma em Float
Out: 10.23

In: 12.to_s   #Transforma em String
Out: "12"

```
##Operador Ternário

```Ruby
def no_limite?
  saldo == saldo + limite ? false : true
end
p no_limite?

```

##GET

```Ruby
puts "Qual é o seu nome?"
nome = gets
print "Seja bem vindo {nome}"
```

##CHOMP PUTS

```Ruby
In: gets  # Testo digitado: Um texto qualquer
Out: "Um texto qualquer\n"

In: gets.chomp # Testo digitado: Um texto qualquer
Out: "Um texto qualquer"
```

##Interpolação


Nos exemplos abaixo foi utilizado o construtor #{}, que serve para substituições de varáveis. Essa técnica é conhecida como interpolation. Note que em ambos os exemplos foram utilizados as aspas duplas. 

```Ruby
In: "Agora é #{Time.now}"
Out: "Agora é 2019-06-27 19:24:27 -0300" 

In: nome = 'jonathan'
In: puts "Meu nome é:  #{nome}"
Out: "Meu nome é:  jonathan" 
```

#Array + Métodos

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
var3.sort #orden a matrix
var3.length #retorno 4
var3.first ou .first 3 #retorno 15 e no caso do .first 3 retorna os 3 primeiros valores.
var3.last #retorno 1
var3.pop #retorno 1 porém o array perde este valor var3 = [15, 24, 189]
var3.push(15) #Adiciona o 15 no final do array
var3.take 3 #retorna os 3 primeiros valores

-----------------------------------------------------------------

string1 = ["some", "thing"]
string2 = ["another", "thing"]
integer1 = [1, 2, 3, 4]
integer2 = [5, 8, 11, 15]
mix1 = [1, 2, ['foo', 'bar']]
mix2 = [[1, 2], ['foo', 'bar']]
m10 = [["a", "b"], ["c", "d"]]
m20 = [[1], [2]]



print integer1.insert(integer1.length, *integer2)
[1, 2, 3, 4, 5, 8, 11, 15]


print mix1.flatten!
[1, 2, "foo", "bar"]

print mix2.flatten!
[1, 2, "foo", "bar"]

print (mix1 << mix2).flatten!
[1, 2, "foo", "bar", 1, 2, "foo", "bar"]


print string1.push(string2.flatten!)
["some", "thing", nil]

---------------------------------------
print string1 + string2
print string1.concat string2
["some", "thing", "another", "thing"]

print string1|integer1
["some", "thing", 1, 2, 3, 4]

print integer1 |= string1
[1, 2, 3, 4, "some", "thing"]

print integer1 += string1
[1, 2, 3, 4, "some", "thing"]

--------------------------------------------

print string1.push(*mix1)
["some", "thing", 1, 2, ["foo", "bar"]]
print string1.unshift(*mix1)
[1, 2, ["foo", "bar"], "some", "thing"]

```
##Detect - Select - Grep - Reject - Uniq

```Ruby
numbers = [1, 2, 3, 4, 5, 6]

# detect é o mesmo que find
#recupera um elemento com base em um critério
detectEle = numbers.detect {|elem| elem % 2 == 0} #retorno o 2 (primeiro divisivel)

# select é o mesmo que find_all
# recupera todos os elementos com base em um critério
selectEle = numbers.select {|elem| elem % 2 == 0} #retorna os divisiveis por 2
divTresCinco = numbers.select {|elem| elem % valor1 == 0 and elem % valor2 == 0} #com operador lógico

# grep
# recupera todos os elementos encontrados para o pattern passado
# em outras palavras recupera os elementos em um intervalo (range)
grepEle = numbers.grep(4..6) #retorna do 4 ao 6.

# Reject
# retira os elementos de um array, segundo uma condição
rejectEle = numbers.reject {|elem| elem % 2 == 0} #retira os divisiveis por 2


# Uniq
# removo elementos duplicados de um array
num = [1, 2, 3, 3, 4, 5, 2, 6]
uniqEle = num.uniq
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

#Divisão
def divisao (primeiro_numero, segundo_numero)
    if segundo_numero == 0 
        return 'Não é possível dividir por zero'
    else 
        return primeiro_numero / segundo_numero
    end
end

divisao(10, 5)



#Retornar a soma das vogais

def vowels_count(frase)
    vogais = frase.downcase.count "aãeiou"
    puts vogais
end

vowels_count('A casa não tem teto')

#Retornar a soma das consoantes

def consonants_count(frase)
    texto = frase.delete(' ')
    txt = texto.downcase.count "aãeiou"
    result = texto.length - txt
    puts result
end

consonants_count("A lua nao")

```
#Blocos e Iterações

```Ruby
#Each

#(do end): é um bloco de código. A variável lang se refere a cada item no array a medida que ele é iterado.

--------------------------------------------

itens = ['Espada', 'Cajado', 'Machado']

itens.each do |lang|
   puts 'Eu uso ' + lang + '!'
   puts 'E você?'
end

'''
Eu uso Espada!
E você?
Eu uso Cajado!
E você?
Eu uso Machado!
E você?
'''

In: 3.times { puts "Olá!" }
Out: Olá!
Out: Olá!
Out: Olá!

--------------------------------------------
     
In: numeros = [1, 2, 3] 
In: numeros.each {|numero| puts numero} 
Out:
1 
2 
3 
=> [1, 2, 3] 
   
--------------------------------------------

In: numeros = [1, 2, 3] 
In: numeros.each do |numero| 
        puts numero 
    end 
Out:
1 
2 
3 
 => [1, 2, 3]  

--------------------------------------------

In: numeros = [1, 2, 3] 
In: numeros.each_with_index do |numero, index| 
        puts "Valor: #{numero}, Índice: #{index}"  
    end 
Out:
Valor: 1, Índice: 0 
Valor: 2, Índice: 1 
Valor: 3, Índice: 2 
 => [1, 2, 3]

--------------------------------------------

def self.multiplica_indices(array)
  array.collect!.with_index { |x, i| x * i }
  return array
end

--------------------------------------------

def tabuada(arg1)
  total = []
  (1..arg1).map do |i|
    valores = []
    (1..10).map do |e|
      valores << e * i
    end
    total << valores
  end
  total
end

```

#Classe



```Ruby
class Monstro
  attr_accessor :energia, :ataque, :vivo

  def initialize
    self.energia = Random.rand(10) + 6
    self.vivo = true
  end

  def bater(alvo)
    if alvo.esta_vivo?
      self.ataque = Random.rand(5)
      puts "O dano do monstro foi #{self.ataque}"
      alvo.energia -= self.ataque
    else
      puts "Você está morto!"
    end
  end

  def esta_vivo?
    true if self.energia > 0
  end
end





class Heroi
  attr_accessor :energia, :ataque, :vivo, :numero_de_mortos

  def initialize
    self.energia = 30
    self.vivo = true
    self.numero_de_mortos = 0
  end



  def bater(alvo)
    if alvo.esta_vivo?
      self.ataque = Random.rand(5) + 3
      puts "O dano do heroi foi #{self.ataque}"
      alvo.energia -= self.ataque
    else
      puts "O monstro está morto!\n\n"
    end
    unless alvo.esta_vivo?
      puts "O monstro está morto!\n\n"
      self.numero_de_mortos += 1
    end
  end

  def esta_vivo?
    true if self.energia > 0
  end

end

--------------------------------------------

class Conta
  attr_accessor :titular, :limite, :saldo, :numero

  def initialize(numero, titular, saldo, limite)
    @numero = numero
    @titular = titular
    @saldo = saldo
    @limite = limite
  end

  def sacar(valor)
    return false if valor > (@saldo + @limite)

    @saldo -= valor
    true
  end

  def depositar(valor)
    @saldo += valor
  end

  def no_limite?
    @saldo < 0
  end

  def ==(conta)
    conta.titular == titular &&
      conta.limite == limite &&
      conta.saldo == saldo &&
      conta.numero == numero
  end

  def transfere(conta_destino, valor_transferencia)
    return false unless sacar(valor_transferencia)

    conta_destino.depositar(valor_transferencia)
  end
end






```




```Ruby


```




```Ruby


```