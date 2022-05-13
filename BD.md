# Banco de dados

## Definição

Cadastra *Dados* em *Registros* definidos em categorias chamados *Campos* a fim de montar uma *Tabela*


| NOME | CIDADE | ENDEREÇO | CARGO | .... | 
| ------- | ------ | ------- |------ | ------ |
| Luiza | Garuva | r. girassol 90 | Compradora | .... |
| Claudia | Joinville | r. pedras 15 | Professora | .... |

Luiza, Claudia = Dado(s)

Linha de Dados = Registro

Nome = Campo

Conjunto de Registros e Campos = Tabela

---
## Tabelas
---

**CHAVE PRIMÁRIA (#,PK)** - Campo que não se repete, caso não existir, inserir campo com um código único

Medico: (NOME,#CRM,DT_NASC,TELEFONE,EMAIL,FOTO,SEXO)

Comida: (#CODCOMIDA,NOME,DESCRICAO,PRECO,VALIDADE,PESO,CALORIAS,INF_NUTRI)

Profissao: (#CODPROF,NOME,DESCRICAO,SALARIO,CARGA_HR)

Hobby: (#CODHOBBY,NOME,DESCRICAO,FREQUENCIA,CUSTO,GASTO_CALORICO)

Namorada: (#CODNAMO,NOME,DESCRICAO,NOTA,SEXO,ALTURA,CABELO,OLHOS,DT_NASC,DT_INI,DT_FIM,CUSTO,TELEFONE,FOTO)

Paciente: (#ID_PCTE,NUMERO_SUS,MATRICULAHOSP,NOME,DESC,DT_NASC,CPF,RG,ALERGIA?,ENDEREÇO)



---
### Relacionamentos

1 - 1 --> uma tabela pode apenas relacionar com uma tabela
1 - N --> uma tabela relaciona com várias
N - N --> várias tabelas podem relacionar com várias
não relacionaveis

**Chave estrangeira (&,FK)** - serve para estabelecer o relacionamento entre duas tabelas

Exemplos:

Medico N ---- N Paciente

Aluno N --- N Disciplina

Nota Fiscal N --- 1 Cliente

Produto N --- N Nota Fiscal

Empregado N ---- 1 Cargo

Produto N --- 1 Tipo de Produto

Médico N --- N Especialidade

Animal N --- 1 Raça

Filme N --- N Gênero

---
## *1º Regra de relacionamentos: 1 -> N*

Chave primaria(#) do lado 1 deve estar SEMPRE na tabela do lado N(&).

Exemplos:
````
Animal N-----------1 Raça
#CodAnimal    -------#IdRaca
Nome          |      Nome
Peso          |      Desc
DtNasc        |
&IdRaca <------
````
````
Nota Fiscal N ------- 1 Cliente
#Nmr_Nota        -------#CPF
Dt               |      Nome
Valor            |      Endereco
Tributos         |      Dt_Nasc
&CPF <------------      Contato
````
````
Estado 1 --------- N Cidade
#UF                #IdCidade
Nome_Estado        Nome 
                   Area
                   Nmr_Bairros
                   Prefeito_Regente
                   Nmr_Vereadores
                   &UF
````
---
## *2º Regra de relacionamentos: N -> N*

Em todo Relacionamento N -> N devemos:

1 - quebrar o relacionamento

2 - criar uma nova tabela (associativa)

3 - Aplicar a 1º regra
````
               na falta de um nome, "junte" o nome da tabelas
                 v
Aluno 1 --- N Aluno_Disciplina N --- 1 Disciplina
````

Exemplos:
````
Receita N ---- 1 Receita-Ingrediente 1 ---- N Ingrediente
#IdReceita--    #IdReceita_Ingrediente    --#IdIngrediente
Nome       |--> &IdReceita                | Nome
                &IdIngrediente <----------| Custo
````
````
Nota Fiscal N ---- 1 Compra 1 ---- N Produto
#NmrNotaFis---      #IdCompra      --#IdProd
Comprador    |----> &NmrNotaFis    | NomeProd
Valor               &IdProd <------| Custo
Imposto                              Imposto
````
````
Produto N ----- 1 Prod-Peça 1 ----- N Peça
#IdProd----      #IdProd_Peça     ----#IdPeça
Nome      |----> &IdProd          |   Nome
Preço            &IdPeça <--------|   Custo
Imposto
````
---
### Exercício:

Elaborar o diagrama de entidades relacionadas bem como identificar os atributos e relacionamentos para cada entidade, para uma escola onde precisamos guardar informações sobre: Turmas, Alunos, Matérias E Professores.

````
Turma 1 -------- N Aluno N -----------1 Matéria-Aluno
  N                                           1
  |                                           |
  1                                           |
Turma-Prof                                    |
  1                                           | 
  |                                           |
  N                                           N        
Prof N -------- 1 Prof-Matéria 1 ------- N Matéria

Turma: (#IdTurma, &Aluno, QntAlunos)
Turma-Prof: (#IdTurma_Prof, &Turma, &Prof, Horario)
Prof: (#IdProf, Nome, Idade)
Prof-Matéria: (#IdProf_Mat, &Prof, &Materia)
Matéria: (#Materia, MediaAprov)
Matéria-Aluno: (#IdMat_Aluno, &Materia, &Aluno, Horario, Nota)
Aluno: (#IdAluno, Nome, idade)
````