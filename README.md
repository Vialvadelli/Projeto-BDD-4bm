# Projeto-BDD-4bm

## 1. Apresentação do projeto

Este projeto tem como objetivo desenvolver um sistema financeiro fictício utilizando a linguagem Python integrada ao banco de dados MongoDB.

O sistema permite registrar receitas e despesas, organizar os lançamentos por categorias e gerar relatórios consolidados, apresentando o total de receitas, despesas e o saldo financeiro.

O projeto também trabalha com conceitos importantes de manipulação e agregação de dados, especialmente o uso de valores monetários com precisão.

## 2. Objetivos

* Registrar receitas e despesas financeiras.
* Classificar os lançamentos por categorias.
* Armazenar os registros no MongoDB.
* Consultar o extrato financeiro.
* Gerar resumos financeiros por tipo e categoria.
* Calcular o saldo final.
* Aplicar operações de agregação do MongoDB.

## 3. Tecnologias utilizadas

* **Python:** linguagem utilizada para desenvolver a aplicação.
* **MongoDB:** banco de dados NoSQL utilizado para armazenar os lançamentos.
* **PyMongo:** biblioteca responsável pela comunicação entre Python e MongoDB.
* **MongoDB Compass:** ferramenta utilizada para visualizar e conferir os documentos armazenados.
* **Decimal:** módulo Python utilizado para garantir maior precisão nos cálculos monetários.

## 4. Estrutura do projeto

```text
repositorio/
│
├── conexao.py
│
└── p05_financas/
    ├── __init__.py
    └── main.py
```

**Descrição dos arquivos:**

* `conexao.py`: estabelece a conexão com o MongoDB e seleciona o banco de dados.
* `main.py`: contém o menu principal e as funcionalidades do sistema financeiro.
* `__init__.py`: identifica a pasta como um pacote Python.

## 5. Funcionamento do sistema

Ao executar o programa, é apresentado um menu interativo com as seguintes opções:

| Opção | Funcionalidade       |
| ----- | -------------------- |
| 1     | Registrar lançamento |
| 2     | Consultar extrato    |
| 3     | Resumo por categoria |
| 0     | Encerrar o programa  |

### 5.1 Registro de lançamentos

O usuário pode cadastrar receitas ou despesas, informando:

* Tipo de lançamento: receita ou despesa.
* Categoria: identificação do lançamento.
* Valor: quantia em reais.

Após a validação das informações, o registro é armazenado na coleção `lancamentos_p05`.

Cada documento possui os seguintes campos:

* `tipo`: identifica se é uma receita ou despesa.
* `categoria`: identifica a categoria financeira.
* `valor_centavos`: armazena o valor em centavos.
* `criado_em`: registra a data e o horário do lançamento.

### 5.2 Consulta do extrato

A opção de extrato consulta os lançamentos armazenados no MongoDB, apresentando os registros mais recentes primeiro.

A consulta utiliza o método `find()`, com ordenação pelo campo `criado_em` e limite de 30 registros.

### 5.3 Resumo por categoria

O sistema utiliza o recurso de agregação do MongoDB para agrupar os lançamentos conforme o tipo e a categoria.

São utilizados os seguintes operadores:

* `$group`: agrupa os lançamentos por tipo e categoria.
* `$sum`: soma os valores armazenados em centavos.
* `$sort`: organiza os resultados por tipo e categoria.

Ao final, o programa apresenta o total de receitas, o total de despesas e o saldo financeiro.

### 5.4 Precisão monetária

Para evitar problemas de precisão em cálculos financeiros, o sistema utiliza o módulo `Decimal` para converter os valores informados em centavos.

Por exemplo:

* R$ 1.500,00 é armazenado como `150000`.
* R$ 200,00 é armazenado como `20000`.
* R$ 100,00 é armazenado como `10000`.

Dessa maneira, os cálculos e as agregações são realizados utilizando números inteiros, evitando imprecisões comuns em operações com números do tipo `float`.

## 6. Execução do programa

Para executar o projeto, é necessário ter Python instalado, acesso a uma instância MongoDB e a biblioteca PyMongo.

Instale a dependência:

```bash
pip install pymongo
```

Configure a conexão com o banco de dados no arquivo `conexao.py`.

Em seguida, execute o comando na raiz do repositório:

```bash
python -m p05_financas.main
```

O banco utilizado é `laboratorio_python`, e a coleção criada pelo programa é `lancamentos_p05`.

## 7. Testes realizados

Para validar o funcionamento do sistema, foram utilizados os seguintes lançamentos:

| Tipo    | Categoria   |       Valor |
| ------- | ----------- | ----------: |
| Receita | Salário     | R$ 1.500,00 |
| Despesa | Alimentação |   R$ 200,00 |
| Despesa | Transporte  |   R$ 100,00 |

### Resultado esperado

| Descrição         |           Valor |
| ----------------- | --------------: |
| Total de receitas |     R$ 1.500,00 |
| Total de despesas |       R$ 300,00 |
| **Saldo final**   | **R$ 1.200,00** |

O saldo é calculado pela seguinte fórmula:

**Saldo = Total de receitas - Total de despesas**

Saldo = 1.500,00 - 300,00

**Saldo = R$ 1.200,00**

O teste permite verificar se os lançamentos foram armazenados corretamente e se a agregação apresenta os valores esperados.

## 8. Evidências do funcionamento

Nesta seção devem ser adicionadas capturas de tela que comprovem a execução e o funcionamento do projeto.

### Evidência 1 – Menu principal

Inserir uma captura de tela mostrando o menu principal do sistema no terminal.

**Descrição:** demonstra as opções disponíveis para interação com o programa.

### Evidência 2 – Registro de receita

Inserir uma captura de tela do cadastro de uma receita de R$ 1.500,00.

**Descrição:** demonstra o registro de uma entrada financeira.

### Evidência 3 – Registro de despesas

Inserir uma captura de tela dos registros das despesas de alimentação e transporte.

**Descrição:** demonstra o cadastro de despesas em categorias distintas.

### Evidência 4 – Consulta do extrato

Inserir uma captura de tela da consulta do extrato financeiro.

**Descrição:** demonstra a recuperação dos lançamentos armazenados no MongoDB.

### Evidência 5 – Resumo por categoria

Inserir uma captura de tela do resultado da agregação, mostrando as receitas, despesas e o saldo final de R$ 1.200,00.

**Descrição:** comprova o funcionamento dos operadores `$group`, `$sum` e `$sort`.

### Evidência 6 – MongoDB Compass

Inserir uma captura de tela do MongoDB Compass mostrando o banco `laboratorio_python` e a coleção `lancamentos_p05`, com os documentos registrados.

**Descrição:** comprova que os dados estão sendo armazenados corretamente no banco de dados.

## 9. Conclusão

O desenvolvimento deste projeto permitiu aplicar conceitos de programação em Python e manipulação de banco de dados MongoDB.

Foi possível compreender como registrar e consultar informações financeiras, realizar agrupamentos por categorias e calcular totais utilizando operações de agregação.

Além disso, a utilização do módulo `Decimal` na conversão dos valores monetários para centavos contribuiu para a precisão dos cálculos financeiros.

O projeto demonstra, na prática, a integração entre Python e MongoDB e a utilização dos operadores de agregação para produzir relatórios financeiros consolidados.

---

**Projeto 05 – Agrupamento e Precisão Monetária**

**Linguagem:** Python
**Banco de dados:** MongoDB
**Biblioteca:** PyMongo
