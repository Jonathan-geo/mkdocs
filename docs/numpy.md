# Numpy
(Introdução ao Numpy)

O NumPy é uma poderosa biblioteca da linguagem de programação Python, pois permite trabalhar, com eficiência, vetores, matrizes, arranjos e permite diversas funçoes e operaçĩes matemáticas. Assim como no python, o Numpy possui um sintaxe clare e objetiva. Dentro da matemática, esta biblioteca permite trabalhar, de forma aplicada, com arrandos multidimencionais, matrizes de n dimensões, álgebra linear, geração de números aleatórios, etc.

Para mais informações sobre o Numpy clique [aqui ](https://www.numpy.org/).

# Instalação - NumPy
Essa biblioteca não é nativa do Python, logo você precisará intalar. Se você baixou o pacote Anaconda, como recomenda na página home desta documentação, o numpy  já estará incluso, caso contrário, você deverá utilizar a ferramenta pip do seu python. Digite o seguinte comando no seu terminal linux ou prompt  windowns.

```python
pip install numpy
```
---
# Let'go to the tutorial?

## Importando a biblioteca
Utilizando o editor de sua preferência como o vsCode, atom ou Pycharme, importe a biblioteca. 

```python
import numpy as np
```
---
## Criando uma Array(Matriz)
No código abaixo podemos observar um exemplo de um list, pois o python não oferece suporte para arrays, porém o Numpy permite que tratemos uma list como um array, como será observado no exemplo 2. 


*Exemplo 1: List*

```python
In [1]: lista = [10,20,40,30]
In [2]: type (lista)

Out[2]: list
```

*Exemplo 2: Numpay Array*

```python
In [1]: Matriz = [10,20,40,30]
In [2]: type (Matriz)

Out[2]: numpy.ndarray
```

## Manipulando Arrays

**Criando uma matriz**

```python

In [1]: m2 = np.array ([[1, 2], [3, 4]])
In [2]: m2

Out[2]: array([[1, 2],
               [3, 4]])

```

**Selecionando elementos de uma matriz**

```python

In [3]: print(m2[0])
Out[3]: [1 2]

In [4]: print(m2[1])
Out[4]: [3 4]

In [5]: print(m2[1][0])
Out[5]: 3

```

**Matriz transposta**

```python

In [3]: print(m2.transpose())
Out[5]: [[1 3]
         [2 4]]

```

**Criando novas matrizes**

```python

In [6]: m3 = np.array([[5,6], [7,8]])
In [7]: m4 = np.array([[1,2], [3,4]])

```
**Somando matrizes**
OBS: as soma, subtração e a multiplicação, funcionam como na geometria. Para manipulações de dadas de modo convencional do python, utilizar uma list.

```python
In [8] print(m3 + m4)
Out[8] [[ 6  8]
        [10 12]]
```

**Somando todos elementos**
OBS: foram somados os elementos da matriz m3, criada logo acima. 

```python
In [9] print (m3.sum())
Out[9] 26
```

**Média Aritmética**


```python
In [10]: print (m4.mean())
Out[10]: 2.5
```

## Fatiamento de Array

**Criando nova matriz**

```python
In [11]: m4 = np.array([[1,2,5,10], [3,4,6,8],[5,7,6,8],[3,2,0,4]])

In [12]: m4
Out[12]:  [[ 1,  2,  5, 10],
           [ 3,  4,  6,  8],
           [ 5,  7,  6,  8],
           [ 3,  2,  0,  4]]
```

**Fatiando a Matriz**

```python
In [13]: print(m4[1:3])

Out[13]:  [[3, 4, 6, 8],
           [5, 7, 6, 8]]
```

```python
In [14]: print(m4[::2])

Out[14]:  [[ 1,  2,  5, 10],
           [ 5,  7,  6,  8]]
```
```python
In [15]: np.array_split(x8,2,axis=0)

Out[15]:  [array([[ 1,  2,  5, 10]]), array([[5, 7, 6, 8]])]
```

## Manipulando termos da Array

**Criando nova matriz**

```python

In [16]: m5 = np.array([[12,2,27,12],[31,4,5,25]])

In [17]: print(m5)
Out[17]:  [[12,  2, 27, 12],
           [31,  4,  5, 25]]
```

**Trocando um termo da matriz**

```python
In [18]: m5[0,0] = 100

In [19]: print(m5)
Out[19]:  [[100,   2,  27,  12]
           [ 31,   4,   5,  25]]
```
**Criando duas matrizes**

```python

In [20]: m6 = np.array([1,2,3])
In [21]: m61 = np.array([4,5,8])

```
**anexar apenas um termo**

```python
In [22]: Result = np.insert(m6, 1, 10)

In [23]: print(Result)
Out[23]:  [ 1 10  2  3]

```

**anexar vários termos**

```python
In [22]: varios = np.append(m6, [10,15,16])

In [23]: print(varios)
Out[23]:  [ 1,  2,  3, 10, 15, 16]

```

**concatenar dois arrays**

```python
In [24]: Result2 = np.concatenate((m6, m61), axis=0)

In [25]: print(Result2)
Out[25]:  [1 2 3 4 5 8]

```
**anexar em dimensões de eixo 0**


```python
In [26]: m7 = np.array([[1,2,3],[5,8,7]])

In [27]: np.append(m7, [[8,8,8]], axis=0)
Out[27]: array([[1, 2, 3],
                [5, 8, 7],
                [8, 8, 8]])

```

**anexar em dimensões de eixo 1**

```python
In [28]: m8 = np.array([[1,2,3],[5,9,7]])

In [29]: np.append(m8, [[8],[8]], axis=1)
Out[29]: array([[1, 2, 3, 8],
                [5, 9, 7, 8]])

```
**deletar termo de uma matriz**

```python
In [30]: m9 = np.array([[1,2],[3,4],[5,6]])
```

```python
#deletando em axis 0
In [31]: np.delete(m9, 1, 0)
Out[31]: array([[1, 2],
                [5, 6]])

```


```python
#deletando em fatiamento(com razão 2)
In [32]: m10 = np.array([[1,2,3],[3,4,7],[5,6,4]0,[4,5,9]])
In [33]: np.delete(m10,np.s_[::2],0)
Out[32]: array([[1, 2],
                [5, 6]])

```


