#python #fastapi #pydantic
A função `model_validate()` é um método de classe que valida e desserializa dados brutos em uma instância do modelo pydantic.

- Ela verifica se os dados fornecidos correspondem ao esquema definido no modelo e, se tudo estiver correto, retorna uma instância do modelo.

```python
from pydantic import BaseModel

class Usuario(BaseModel):
	id: int
	nome: str
	idade: int
	
dados_brutos = {"id": 1, "nome": "João", "idade": 30}
usuario = Usuario.model_validate(dados_brutos)
print(usuario)
...
```

- Caso os dados informados não sejam válidos, uma exceção `ValidationError` é lançada:

```python
...

dados_invalidos = {"id": "um", "nome": "João", "idade": 30}

try:
    usuario_invalido = Usuario.model_validate(dados_invalidos)
except ValidationError as e:
      print(e)
      
"""
1 validation error for Usuario
id
  Input should be a valid integer, unable to parse string as an integer [type=int_parsing, input_value='um', input_type=str]
"""
```

**Quando usar o model_validate()?**

- Quando se recebe dados brutos (requisição HTTP, banco de dados ou arquivo) e é necessário convertê-los em um objeto Pydantic.
- Para garantir que os dados estejam de acordo com o esquema definido no modelo.
- Para validar e desserializar dados de entrada em uma API RESTful