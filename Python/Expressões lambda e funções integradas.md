#python
### Lambdas
Expressões Lambda são uma forma concisa de criar funções anonimas (sem nome). Elas são frequentemente usada para definir pequenas funções que serão utilizadas poucas vezes ou em situações onde não é necessário nomeá-las explicitamente.

**Sintaxe básica**
`lambda argumentos: expressão`

- lambda: palavra-chave que define uma função anônima.
- argumentos: os parâmetros que a função aceita, separados por vírgulas.
- expressão: o retorno da função, que deve ser uma única expressão.

```python
soma = lambda x, y: x + y
print(soma(3, 5)) # Saída: 8
```

No exemplo acima está um exemplo básico de utilização de lambdas em Python. Não é das formas mais intuitivas de utilizá-lo, pois a função anônima tá sendo atribuída a uma variável para depois ser chamada. A melhor forma de se utilizar lambdas é utilizá-las com funções integradas.
### Funções integradas
#### Map
O map é uma função que tem como objetivo aplicar uma função em todos os itens de um elemento iterável. Ela recebe dois parâmetros, uma função e uma coleção.

- Ela retorna um **Map Object**, que pode ser convertido em uma coleção.
- Em tempo de execução, o Map Object só pode ser convertido uma única vez, após a primeira exibição, o Map Object é zerado.
```python
numeros = [1, 2, 3, 4, 5]
quadrados = map(lambda x: x**2, numeros)
print(list(quadrados))
```

Outro exemplo de uso com map

```python
cidades = [("Berlim", 29), ("Cairo", 36), ("Los Angeles", 26), ("Tokio", 27)]

cidades_temperatura_f = map(lambda item: (item[0], (9/5) * item[1] + 32), cidades)

print(list(cidades_temperatura_f))

# [('Berlim', 84.2), ('Cairo', 96.8), ('Los Angeles', 78.80000000000001), ('Tokio', 80.6)]
```
#### Filter
O filter, como o nome já diz, filtra dados segundo alguma regra. Assim como o map, ele recebe dois parâmetros, uma função e uma coleção.
- No filter, a função terá alguma regra que separará os valores do elemento iterável passado e retornará um **Filter Object** com os itens que atendem a condição passada.
    - O filter object, assim como o map object pode ser convertido para uma coleção.
- Assim como o Map Object, o Filter Object só pode ser convertido uma única vez, após a primeira execução, eles são excluídos da memória.

```python
dados = [2.9, 3.9, 4.2, 4.5, 8.4, 6.3, 9.5, 3.2, 5, 2, 7]

dados_acima_media = filter(lambda item: item > 6, dados) # Criará um objeto com todos os itens que são maiores que 6.

print(list(dados_acima_media)) 
```

É possível também utilizar o filter para remover dados em branco sem utilizar lambdas

```python
data = ["", "Brasil", "Peru", "", "", "Cuba", "", "Jamaica", "México"]

paises = filter(None, data)
paises = filter(lambda item: len(item) > 0, data) # Alternativa utilizando lambda

print(list(paises))

```

#### Reduce
O reduce consiste em diversos passos, passando por cada item do iterável, visando acumular valores e retornar o valor total.

- O reduce recebe uma função e um iterável, como o map e o filter, com uma diferença, a função recebe dois parâmetros.
- A função é aplicada ao primeiro par de elementos do iterável. O resultado dessa operação é então combinado com o próximo elemento, e assim por diante, até que todos os elementos tenham sido processados.
- O valor retornado de um reduce não é necessário qualquer conversão.

A partir do Python3+ a função `reduce()` não é mais uma função integrada (built-in). Agora é necessário importar e utilizar esta função a partir do módulo `functools`.

> Segundo Guido Van Rossum, é mais recomendado utilizar um loop for por ser mais legível, contudo, pode-se usar a função reduce se realmente for necessário.

```python
from functools import reduce

dados = [2, 4, 6, 3, 5, 9, 7]

total = reduce(lambda x, y: x + y, dados)

print(total) # 36
```

#### All
Verifica todos os elementos de uma lista e retorna `True` se todos os elementos forem verdadeiros ou `False` se essa condição não for correspondida.

- Retorna `True` também se o iterável estiver vazio

```python
print(all([0, 1, 2, 3, 4]) # Retorna False pois 0 é False

print(all((2, 4, 5, 6, 8)) # Retorna True

nomes = ["João", "Jamile", "Joaquim", "Maria"]
print(all([nome[0] == "J" for nome in nomes])) # Verifica todos os itens na lista 'nomes' começam com a letra 'J' e retorna True ou False.
```
Necessário cuidado, pois um iterável vazio tem valor False.
#### Any
Verifica todos os elementos do iterável e retorna `True` se qualquer elemento for Verdadeiro ou `False` se essa condição não for correspondida ou o iterável estiver vazio.

```python
nomes = ["João", "Jamile", "Joaquim", "Maria"]
print(any([nome[0] == "M" for nome in nomes])) # Verifica todos os itens na lista 'nomes' começam com a letra 'J' e retorna True ou False.
```
#### Generator
Generator é uma forma de criar itens iteráveis de uma forma especial, consumindo menos memória em comparação com listas e outras estruturas de dados tradicionais.
- Eles permitem a geração de valores **sob demanda**, ou seja, os valores são produzidos apenas quando necessários, o que os torna muito úteis para trabalhar com grandes volumes de dados.

```python
 gen = (x**2 for x in range(5))
```
#### Sorted
A função `sorted()` permite ordenar qualquer iterável. Criando uma lista com os itens ordenados, não modificando o iterável onde estão os dados.
- É diferente do método sort(), que funciona apenas em listas.
#### Demais Funções
- `len()`: Retorna o tamanho (o número de itens) de um iterável
- `abs()`: Retorna o valor absoluto (o seu valor desconsiderando o sinal) de um número inteiro ou real.
- `sum()`: Recebe como parâmetro um iterável, podendo receber também um valor inicial e retorna a soma dos valores do iterável, adicionando também o valor inicial
- `round()`: Retorna um número arredondado para n digital de precisão após a cada decimal, se a precisão não for informada, retorna o inteiro mais próximo da entrada.
---
### EXTRA: Função Next
A função `next()` é uma poderosa ferramenta que permite acessar elementos de um iterador. Ela é especialmente útil quando se trabalha com estruturas de dados que podem ser iteradas, como listas, tuplas, conjuntos e generators.
- Seu principal uso é para **obter o próximo elemento de um iterador**. Ela recebe um iterador como argumento e retorna o próximo elemento desse iterador. Caso não haja mais elementos disponíveis, ele retorna a exceção `StopIreration`.
- Ela pode receber também um segundo parâmetro default, que é exibido caso não haja mais itens para ser iterado. Assim, é possível trazer uma mensagem mais agradável.

**Sintaxe principal**

`next(iterador, default)`

```python
available_profile = next(
    (
        perfil
        for perfil in user.perfil
        if perfil.tipo_perfil == profile_to_update.value
    ),
    None,
)
```

> A função `next` no exemplo acima é usada para obter o primeiro item do generator que atende a condição proposta (tipo do perfil igual ao perfil para ser atualizado). Caso nenhum atenda, ele retornará `None`.

A vantagem principal da função **next()** é consumir os valores de um iterador sob demanda, ao invés de carregar todos os valores na memória ao mesmo tempo. Isso é essencial ao trabalhar com grandes volumes de dados ou fluxos infinitos.

**Conclusão**

Embora o loop `for()` seja geralmente mais simples e legível, em alguns casos, o uso da função `next()` pode fornecer mais flexibilidade e otimização de memória durante o processo de iteração. É uma ferramenta versátil e poderosa para trabalhar com iteradores, pois permite acessar os elementos de uma estrutura de dados de forma controlada. Trabalhar com a função `next()` permite escrever um código mais robusto, legível e escalável.