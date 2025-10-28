# Padrões de Desenvolvimento Python

Este documento define os padrões para desenvolvimento, organização e manutenção de projetos Python na empresa. Seguir estes padrões garante código mais legível, sustentável e de fácil manutenção por toda a equipe.

---

## 1. Nomenclatura de Métodos e Funções

- **Use o padrão snake_case** para nomes de funções e métodos.  
  Exemplo: `get_user_data`, `process_payment`, `send_email`

- **Comece o nome de funções e métodos com um verbo** que indique a ação realizada, sempre que possível.
  - Exemplo correto: `create_invoice`, `update_order_status`
  - Exemplo a evitar: `invoice_creator`, `order_status_update`

- Nomes devem ser **claros, descritivos e concisos**. Evite abreviações desnecessárias.

---

## 2. Nomenclatura de Variáveis

- Variáveis devem usar **snake_case** e ter nomes descritivos.
  - Exemplo: `total_amount`, `user_id`, `file_path`
- Evite nomes genéricos como `data`, `info`, `var`, `tmp`, exceto em contextos muito locais.
- Use nomes em inglês, salvo exceções de domínio do negócio.
- Para constantes, use **UPPER_SNAKE_CASE**.
  - Exemplo: `MAX_RETRIES`, `DEFAULT_TIMEOUT`

---

## 3. Números Mágicos

- **Evite números mágicos** (valores numéricos usados diretamente no código sem significado explícito).
  - Em vez disso, defina constantes com nomes descritivos no início do arquivo, ou em um módulo de configurações/constantes.
  - Exemplo ruim:
    ```python
    if attempts > 3:
        ...
    ```
  - Exemplo bom:
    ```python
    MAX_ATTEMPTS = 3
    if attempts > MAX_ATTEMPTS:
        ...
    ```

---

## 4. Tipagem (Type Hints)

- Sempre que possível, utilize **type hints** em funções, métodos, variáveis e atributos de classes para facilitar a leitura, manutenção e integração com ferramentas de análise estática (ex: mypy, Pyright).
- Exemplos:
    ```python
    def calculate_total(price: float, quantity: int) -> float:
        return price * quantity

    user_id: int = 123
    user_name: str = "João"

    from typing import List, Dict, Optional

    def get_users() -> List[Dict[str, str]]:
        ...

    def find_user(user_id: int) -> Optional[User]:
        ...
    ```
- Tipar variáveis de instância em classes usando **PEP 526**:
    ```python
    class Order:
        id: int
        total: float

        def __init__(self, id: int, total: float):
            self.id = id
            self.total = total
    ```
- Priorize o uso de tipagem explícita em APIs públicas, funções utilitárias, e código compartilhado entre equipes.
- Utilize ferramentas de verificação de tipo (mypy, Pyright) no pipeline de CI sempre que possível.

---

## 5. Princípios de Clean Code e SOLID

- **Código limpo (Clean Code):**
  - Escreva funções curtas, que realizam uma única tarefa.
  - Dê nomes claros para variáveis, funções, classes e arquivos.
  - Comente apenas o necessário. O código deve ser autoexplicativo.
  - Prefira composição a herança quando possível.
  - Elimine código morto e evite complexidade desnecessária.

- **Princípios SOLID:**
  - **S**ingle Responsibility: cada classe/função deve ter uma responsabilidade única.
  - **O**pen/Closed: código deve ser aberto para extensão, fechado para modificação.
  - **L**iskov Substitution: subclasses devem ser substituíveis por suas superclasses.
  - **I**nterface Segregation: prefira várias interfaces específicas a uma geral.
  - **D**ependency Inversion: dependa de abstrações, não de implementações concretas.

---

## 6. Evitar Duplicidade de Código

- Antes de criar uma nova função/método, verifique se já existe funcionalidade semelhante no projeto.
- Extraia lógicas repetidas para funções utilitárias ou mixins.
- Utilize herança e composição de forma criteriosa para compartilhar código.

---

## 7. Estrutura de Pastas para Novos Projetos

Siga a seguinte estrutura básica para projetos Django/Python:

```
meu_projeto/
│
├── manage.py
├── requirements.txt
├── README.md
├── .env.example
├── docker-compose.yml
│
├── meu_projeto/           # pasta do settings do Django
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
│
├── apps/                  # cada app Django fica aqui
│   ├── __init__.py
│   ├── core/
│   │   ├── models.py
│   │   ├── views.py
│   │   └── ...
│   └── ...
│
├── utils/                 # funções utilitárias e helpers
│   ├── __init__.py
│   └── ...
│
├── tests/                 # testes unitários e de integração
│   ├── __init__.py
│   └── ...
│
├── scripts/               # scripts para tarefas administrativas
│   └── ...
│
└── docs/                  # documentação do projeto
    └── ...
```

- Cada app Django deve estar dentro da pasta `apps/`.
- Funções utilitárias compartilhadas ficam em `utils/`.
- Testes separados em `tests/`.
- Use `requirements.txt` ou `Pipfile` para dependências.
- Versione um arquivo `.env.example` para configuração de ambiente.

---

## 8. Outras Boas Práticas

- Siga a [PEP8](https://peps.python.org/pep-0008/) para formatação.
- Sempre escreva testes para novas funcionalidades e correções.
- Utilize ferramentas de lint (ex: flake8, black) e análise estática.
- Prefira variáveis e funções em inglês salvo exceções de domínio do negócio.

---

## 9. Referências

- [PEP8 - Python Style Guide](https://peps.python.org/pep-0008/)
- [PEP 484 - Type Hints](https://peps.python.org/pep-0484/)
- [PEP 526 - Variable Annotations](https://peps.python.org/pep-0526/)
- [Clean Code Book](https://www.goodreads.com/book/show/3735293-clean-code)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [Django Project Structure](https://docs.djangoproject.com/en/4.2/)

---
