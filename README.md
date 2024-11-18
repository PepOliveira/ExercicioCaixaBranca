# ExercicioOhata

COMPLEXIDADE CICLOMÁTICA COM CALCULOS
M = E - N + 2P
M=E−N+2P
M=13−13+2(1)M = 13 - 13 + 2(1)
M=13−13+2(1)
M=2M = 2
M=2

A complexidade ciclomática calculada é 2, o que significa que existem dois caminhos independentes no código:

- Um caminho onde a condição `if (rs.next())` é verdadeira.
- Um caminho onde a condição `if (rs.next())` é falsa.

CAMINHOS INDEPENDENTES

**Método `conectarBD()`**
- **Caminho 1**:  (`1 → 2 → 3 → 5`).
- **Caminho 2**:  (`1 → 2 → 3 → 4 → 5`).

**Método `verificarUsuario()`**:
- **Caminho 1**: nesse caminho o  `conectarBD()` é chamado e a execução da SQL é bem-sucedida com `rs.next()` true (`6 → 7 → 8 → 9 → 10 → 11 → 13`).
- **Caminho 2**: nesse caminho o `rs.next()` é false (`6 → 7 → 8 → 9 → 10 → 12 → 13`).
- **Caminho 3**: nesse caminho ocorre uma exceção durante a execução do `try` (`6 → 7 → 8 → 9 → 12 → 13`).
- **Caminho 4**: aqui é execução com falha na conexão (`6 → 7` com `conn` nulo levando a retorno imediato).

- no método `verificarUsuario()` é 4 a complexidade ciclomática, indicando que existem 4 caminhos independentes que precisam ser testados.
- no método `conectarBD()` é 2 a complexidade ciclomática, indicando 2 caminhos principais.

CAMINHOS INDEPENDENTES

**Caminho 1: execução bem-sucedida com `rs.next()` true**
1 → 2 → 3 → 4 → 5 → 6 (entra no bloco `if`) → 7 → 9.

**Caminho 2: execução bem-sucedida com `rs.next()` false**
1 → 2 → 3 → 4 → 5 → 6 (não entra no bloco `if`) → 9.

**Caminho 3: exceção durante a execução da consulta**
1 → 2 → 3 → 4 → 8 → 9.

**Caminho 4: falha com a conexão do banco de dados**
1 → 2 (retorna `null`) → 9.

GRAFO DE FLUXO AQUI:

[GRAFO DE FLUXO OHATA.pdf](https://github.com/user-attachments/files/17804766/GRAFO.DE.FLUXO.OHATA.pdf)


