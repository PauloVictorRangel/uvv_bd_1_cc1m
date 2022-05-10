# Design e Desenvolvimento de Bancos de Dados

---
## Pset 2
 
*Aluno:* Paulo Victor Rangel da Silva Cruz

*Professor:* Abrantes Araújo Silva Filho

*Monitoria:* Suellen Miranda Amorim

*Turma:* CC1M

---

# Introdução

Este Pset tem como objetivo que os estudantes façam relatórios para uma empresa fictícia, mas assim aprendemos sobre algebra relacional, aprimorando nosso aprendizado.

## ⚠️Aviso!!
Este Pset é dependente do [Pset1]( https://github.com/PauloVictorRangel/uvv_bd_1_cc1m/tree/main/PSet1), em particular, o script do MySQL que foi usado para fazer os comandos da atividade.

---

# Questões 

---

## Questão 1 :

Prepare um relatório que mostre a média salarial dos funcionários
de cada departamento.

#### SQL
SELECT numero_departamento, AVG(salario) as media_de_cada_departamento
FROM funcionario
GROUP BY numero_departamento;


---

## Questão 2 :

Prepare um relatório que mostre a média salarial dos homens e das
mulheres.

#### SQL
SELECT sexo, AVG(salario) as media_salarial
FROM funcionarios
GROUP BY sexo;


---

## Questão 3 :

Prepare um relatório que liste o nome dos departamentos e, para
cada departamento, inclua as seguintes informações de seus funcionários: o nome
completo, a data de nascimento, a idade em anos completos e o salário.

#### SQL
SELECT departamentos.nome_departamento, concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as nome, funcionarios.data_nascimento,  year(curdate()) - year(data_nascimento) as idade, funcionarios.salario as salario 
FROM departamentos
INNER JOIN funcionarios ON departamentos.numero_departamento=funcionarios.numero_departamento;


---

## Questão 4 :

Prepare um relatório que mostre o nome completo dos funcioná-
rios, a idade em anos completos, o salário atual e o salário com um reajuste que
obedece ao seguinte critério: se o salário atual do funcionário é inferior a 35.000 o
reajuste deve ser de 20%, e se o salário atual do funcionário for igual ou superior a
35.000 o reajuste deve ser de 15%.

#### SQL
SELECT concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as nome, funcionarios.data_nascimento, year(curdate()) - year(data_nascimento) as idade, salario as salario_atual, salario*1.2 as salario_reajustado
FROM funcionarios
WHERE salario < 35.000
Union
SELECT concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as nome, funcionarios.data_nascimento, year(curdate()) - year(data_nascimento) as idade, salario as salario_atual, salario*1.15 as salario_reajustado 
FROM funcionarios
WHERE salario >= 35.000;


---

## Questão 5 :

Prepare um relatório que liste, para cada departamento, o nome
do gerente e o nome dos funcionários. Ordene esse relatório por nome do depar-
tamento (em ordem crescente) e por salário dos funcionários (em ordem decres-
cente).

#### SQL
SELECT departamentoss.nome_departamento, 
CASE WHEN departamentos.cpf_gerente=funcionarios.cpf
THEN concat(primeiro_nome," ", nome_meio,".",ultimo_nome)
END as Gerente,
concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as funcionarios
FROM departamentos
INNER JOIN funcionarios ON departamentos.numero_departamento=funcionarios.numero_departamento
GROUP BY nome_departamento ASC, salario DESC;


---

## Questão 6 :

Prepare um relatório que mostre o nome completo dos funcioná-
rios que têm dependentes, o departamento onde eles trabalham e, para cada funci-
onário, também liste o nome completo dos dependentes, a idade em anos de cada
dependente e o sexo (o sexo NÃO DEVE aparecer como M ou F, deve aparecer
como “Masculino” ou “Feminino”)

#### SQL
SELECT departamentos.nome_departamento,
concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as funcionario_com_dependente,
concat(dependentes.nome_dependente," ", funcionarios.nome_meio,".",funcionarios.ultimo_nome) as dependente,
year(curdate()) - year(dependentes.data_nascimento) as idade_dependente,
CASE dependentes.sexo
WHEN 'M' THEN 'Masculino'
WHEN 'F' THEN 'Feminino'
END as sexo_dependente
FROM funcionarios
INNER JOIN dependentes ON dependentes.cpf_funcionario=funcionarios.cpf
INNER JOIN departamentos ON departamentos.numero_departamento = funcionarios.numero_departamento;


---

## Questão 7 :

Prepare um relatório que mostre, para cada funcionário que **NÃO
TEM** dependente, seu nome completo, departamento e salário.

#### SQL
SELECT departamentos.nome_departamento, concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as nome, salario
FROM funcionarios
INNER JOIN departamentos ON funcionarios.numero_departamento=departamentos.numero_departamento
LEFT JOIN dependentes ON funcionarios.cpf=dependentes.cpf_funcionario
WHERE dependentes.nome_dependente is null;


---

## Questão 8 :

Prepare um relatório que mostre, para cada departamento, os projetos desse departamento e o nome completo dos funcionários que estão alocados
em cada projeto. Além disso inclua o número de horas trabalhadas por cada funcionário, em cada projeto.

#### SQL
SELECT departamentos.nome_departamento, 
concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as funcionario,
trabalha_em.numero_projeto as nº_projeto, projeto.nome_projeto as nome_do_projeto, trabalha_em.horas as horas_trabalhadas
FROM funcionarios
INNER JOIN departamentos ON departamentos.numero_departamento=funcionarios.numero_departamento
LEFT JOIN projeto ON funcionarios.numero_departamento=projeto.numero_departamento
LEFT JOIN trabalha_em ON projeto.numero_projeto=trabalha_em.numero_projeto
WHERE funcionarios.cpf=trabalha_em.cpf_funcionario
ORDER BY departamentos.nome_departamento DESC;


---

## Questão 9 :

Prepare um relatório que mostre a soma total das horas de cada
projeto em cada departamento. Obs.: o relatório deve exibir o nome do departamento, o nome do projeto e a soma total das horas.

#### SQL
SELECT departamentos.nome_departamento, projeto.nome_projeto, SUM(trabalha_em.horas) as horas_somadas
FROM trabalha_em
INNER JOIN projeto ON trabalha_em.numero_projeto = projeto.numero_projeto
INNER JOIN departamentos ON departamentos.numero_departamento = projeto.numero_departamento
GROUP BY departamentos.nome_departamento, projeto.nome_projeto;


---

## Questão 10 :

Prepare um relatório que mostre a média salarial dos funcionários
de cada departamento.

#### SQL
SELECT numero_departamento, AVG(salario) as media_de_cada_departamento
FROM funcionarios
GROUP BY numero_departamento;


---

## Questão 11 :

Considerando que o valor pago por hora trabalhada em um projeto
é de 50 reais, prepare um relatório que mostre o nome completo do funcionário, o
nome do projeto e o valor total que o funcionário receberá referente às horas trabalhadas naquele projeto.

#### SQL
SELECT concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as funcionario, projeto.nome_projeto, (trabalha_em.horas * 50) as valor_total, trabalha_em.horas as horas_trabalhadas
FROM funcionarios
INNER JOIN trabalha_em ON trabalha_em.cpf_funcionario = funcionarios.cpf
INNER JOIN projeto ON projeto.numero_projeto = trabalha_em.numero_projeto
ORDER BY nome_projeto;


---

## Questão 12 :

Seu chefe está verificando as horas trabalhadas pelos funcionários
nos projetos e percebeu que alguns funcionários, mesmo estando alocadas à algum
projeto, não registraram nenhuma hora trabalhada. Sua tarefa é preparar um relatório que liste o nome do departamento, o nome do projeto e o nome dos funcionários que, mesmo estando alocados a algum projeto, não registraram nenhuma hora trabalhada.

#### SQL
SELECT departamentos.nome_departamento, projeto.nome_projeto, concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as funcionario, trabalha_em.horas
FROM trabalha_em
INNER JOIN funcionarios ON trabalha_em.cpf_funcionario = funcionarios.cpf
INNER JOIN projeto ON trabalha_em.numero_projeto = projeto.numero_projeto
INNER JOIN departamentos ON departamentos.numero_departamento = funcionarios.numero_departamento
WHERE trabalha_em.horas = 0;


---

## Questão 13 :

Durante o natal deste ano a empresa irá presentear todos os fun-
cionários e todos os dependentes (sim, a empresa vai dar um presente para cada
funcionário e um presente para cada dependente de cada funcionário) e pediu para
que você preparasse um relatório que listasse o nome completo das pessoas a serem
presenteadas (funcionários e dependentes), o sexo e a idade em anos completos
(para poder comprar um presente adequado). Esse relatório deve estar ordenado
pela idade em anos completos, de forma decrescente.

#### SQL
SELECT
concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as funcionarios,
year(curdate()) - year(funcionarios.data_nascimento) as idade_funcionario,
concat(dependentes.nome_dependente," ", funcionarios.nome_meio,".",funcionarios.ultimo_nome) as dependente,
year(curdate()) - year(dependentes.data_nascimento) as idade_dependente,
CASE dependentes.sexo
WHEN 'M' THEN 'Masculino'
WHEN 'F' THEN 'Feminino'
END as sexo_dependente
FROM funcionarios
LEFT JOIN dependente ON dependentes.cpf_funcionario=funcionarios.cpf
GROUP BY idade_funcionario DESC, idade_dependente DESC;


---

## Questão 14 :

Prepare um relatório que exiba quantos funcionários cada departamento tem.

#### SQL
SELECT departamentos.nome_departamento, count(funcionarios.cpf) as Total_Funcionarios
FROM departamentos
INNER JOIN funcionario ON funcionario.numero_departamento = departamentoss.numero_departamento
GROUP BY departamentos.nome_departamento, departamentos.numero_departamento, funcionarios.numero_departamento
ORDER BY Total_Funcionarios DESC;


---

## Questão 15 :

Como um funcionário pode estar alocado em mais de um projeto,
prepare um relatório que exiba o nome completo do funcionário, o departamento
desse funcionário e o nome dos projetos em que cada funcionário está alocado.
Atenção: se houver algum funcionário que não está alocado em nenhum projeto,
o nome completo e o departamento também devem aparecer no relatório.

#### SQL
SELECT concat(primeiro_nome," ", nome_meio,".",ultimo_nome) as funcionarios, funcionarios.numero_departamento, projeto.nome_projeto
FROM funcionarios
LEFT JOIN trabalha_em ON trabalha_em.cpf_funcionario = funcionarios.cpf
LEFT JOIN projeto ON projeto.numero_projeto=trabalha_em.numero_projeto;


---

# Declarações

Foi um pouco satisfatório fazer este Pset, na hora de colocar o comando e ver ele funcionando é a melhor parte disparado.
