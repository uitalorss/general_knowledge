#python #backend #datastructure
Comprehensions são construções concisas e expressivas que permitem criar novas sequências () ou iterar sore elas de maneira eficiente. São úteis para simplificar loops tradicionais e tornar o código mais legível e compacto.

**Itens presentes em todas os tipos de comprehension**

- iterável: Qualquer objeto que pode ser iterado (listas, tuplas, conjuntos).
- condição (opcional): Filtro para incluir somente elementos que satisfaçam a condição.

### List Comprehension

Permite criar listas a partir de sequências iteráveis, aplicando condições ou transformações.

**Sintaxe básica**

```python
comprehension = [expressao for item in iteravel if condicao]
```

- expressão: Transformação ou valor que será incluído na lista.
- Demais itens no tópico **Itens presentes em todas os tipos de comprehension**

**Exemplo prático:** Uma lista com os quadrados dos números pares de 0 a 9

```python
# TRADICIONAL
numeros = []
for i in range(10):
    if i % 2 == 0:
        numeros.append(i ** 2)

# COMPREHENSION
numeros = [value ** 2 for value in range(10) if value % 2 == 0]
```

### Dict Comprehension

E uma maneira de criar dicionários a partir de iteráveis, definindo dinamicamente as chaves e valores de um dicionário com base em uma expressão, possivelmente aplicando condições para filtrar os elementos.

**Sintaxe básica**

```python
{chave:valor for item in iteravel if condicao}
```

- chave: Define a chave do dicionário
- valor: Define o valor correspondente à chave.
- Demais itens no tópico **Itens presentes em todas os tipos de comprehension**

Exemplo: Dicionários com números e seus quadrados:

```python
quadrados = {x: x**2 for x in range(5)}
print(quadrados)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

Exemplo: Dicionários com números pares e seus quadrados.

```python
pares_quadrados = {x: x**2 for x in range(10) if x % 2 == 0}
print(pares_quadrados)  # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

### Set Comprehension

É uma estrutura semelhante as list comprehension, com o detalhe de que não permite dados duplicados.

**Sintaxe básica**

```python
comprehension = {expressao for item in iteravel if condicao}
```

- expressão: Transformação ou valor que será incluído no conjunto.

Demais itens no tópico **Itens presentes em todas os tipos de comprehension**

**Exemplo: Remover dados duplicados em uma lista.**

```python
lista = [1, 2, 2, 3, 4, 4, 5]
conjunto = {x for x in lista}
print(conjunto) # {1, 2, 3, 4, 5} 
```

### Conclusão

Comprehensions em Python são ferramentas poderosas que permitem criar e manipular coleções de maneira eficiente, elegante e expressiva. Seja trabalhando com listas, dicionários, conjuntos ou geradores, elas simplificam operações comuns, como filtragem, transformação e criação de estruturas baseadas em iteráveis. Além de melhorarem a legibilidade do código, contribuem para uma escrita mais compacta e direta, reduzindo a necessidade de loops explícitos e construções auxiliares.

No entanto, é importante usá-las com equilíbrio: compreensões muito complexas podem comprometer a clareza do código. Para situações mais sofisticadas ou com lógica intricada, loops tradicionais podem ser mais adequados.