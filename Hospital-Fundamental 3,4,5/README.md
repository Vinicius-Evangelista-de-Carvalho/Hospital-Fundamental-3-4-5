# Hospital-Fundamental
Nesse projeto proposto pelo professor Gabriel Augusto da faculdade Flamingo, criei o banco de dados de um hospital. Analisei o objetivo do meu banco de dados e as informações que eu iria necessitar para modelar e estruturar o banco.

<h3>Parte 1: Diagrama Entidade Relacionamento</h3>
<br>
<p>
Analise a seguinte descrição e extraia dela os requisitos para o banco de dados:
O hospital necessita de um sistema para sua área clínica que ajude a controlar consultas realizadas. Os médicos podem ser generalistas, especialistas ou residentes e têm seus dados pessoais cadastrados em planilhas digitais. Cada médico pode ter uma ou mais especialidades, que podem ser pediatria, clínica geral, gastroenterologia e dermatologia. Alguns registros antigos ainda estão em formulário de papel, mas será necessário incluir esses dados no novo sistema.

Os pacientes também precisam de cadastro, contendo dados pessoais (nome, data de nascimento, endereço, telefone e e-mail), documentos (CPF e RG) e convênio. Para cada convênio, são registrados nome, CNPJ e tempo de carência.

As consultas também têm sido registradas em planilhas, com data e hora de realização, médico responsável, paciente, valor da consulta ou nome do convênio, com o número da carteira. Também é necessário indicar na consulta qual a especialidade buscada pelo paciente.

Deseja-se ainda informatizar a receita do médico, de maneira que, no encerramento da consulta, ele possa registrar os medicamentos receitados, a quantidade e as instruções de uso. A partir disso, espera-se que o sistema imprima um relatório da receita ao paciente ou permita sua visualização via internet.
</p>
<br>
<img src='DiagramaER-1.png' align="center"/>
<br>
<h3>Parte 2: Diagrama Entidade Relacionamento</h3>
<br>
<p>
No hospital, as internações têm sido registradas por meio de formulários eletrônicos que gravam os dados em arquivos. 

Para cada internação, são anotadas a data de entrada, a data prevista de alta e a data efetiva de alta, além da descrição textual dos procedimentos a serem realizados. 

As internações precisam ser vinculadas a quartos, com a numeração e o tipo. 

Cada tipo de quarto tem sua descrição e o seu valor diário (a princípio, o hospital trabalha com apartamentos, quartos duplos e enfermaria).

Também é necessário controlar quais profissionais de enfermaria estarão responsáveis por acompanhar o paciente durante sua internação. Para cada enfermeiro(a), é necessário nome, CPF e registro no conselho de enfermagem (CRE).

A internação, obviamente, é vinculada a um paciente – que pode se internar mais de uma vez no hospital – e a um único médico responsável.
</p>
<br> 
<img src='DiagramaER-2.png' align="center"/>

<h3>Parte 3 - Alimentando o banco de dados</h3>
<p> Crie scripts de povoamento das tabelas desenvolvidas na atividade anterior. Observe as seguintes atividades: </p>
<ul>
<li>Inclua ao menos dez médicos de </li>
<li>Ao menos sete especialidades (considere a afirmação de que “entre as especialidades há pediatria, clínica geral, gastroenterologia e dermatologia”).</li>
<li>Inclua ao menos 15 pacientes. </li>
<li>Registre 20 consultas de diferentes pacientes e diferentes médicos (alguns pacientes realizam mais que uma consulta). As consultas devem ter ocorrido entre 01/01/2015 e 01/01/2022. Ao menos dez consultas devem ter receituário com dois ou mais medicamentos. </li>
<li>Inclua ao menos quatro convênios médicos, associe ao menos cinco pacientes e cinco consultas. </li>
<li>Criar entidade de relacionamento entre médico e especialidade.  </li>
<li>Criar Entidade de Relacionamento entre internação e enfermeiro.  </li>
<li>Arrumar a chave estrangeira do relacionamento entre convênio e médico. </li>
<li>Criar entidade entre internação e enfermeiro. </li>
<li>Colocar chaves estrangeira dentro da internação (Chaves Médico e Paciente). </li>
<li>Registre ao menos sete internações. Pelo menos dois pacientes devem ter se internado mais de uma vez. Ao menos três quartos devem ser cadastrados. As internações devem ter ocorrido entre 01/01/2015 e 01/01/2022. </li>
<li>Considerando que “a princípio o hospital trabalha com apartamentos, quartos duplos e enfermaria”, inclua ao menos esses três tipos com valores diferentes. </li>
<li>Inclua dados de dez profissionais de enfermaria. Associe cada internação a ao menos dois enfermeiros. </li>
<li>Os dados de tipo de quarto, convênio e especialidade são essenciais para a operação do sistema e, portanto, devem ser povoados assim que o sistema for instalado. </li>
</ul>
<br>

# Hospital

<img src='hospital.png'/>

# Médico

<img src='medico.png'/>

# Consulta

<img src='consulta1.png'/>

# Cargo
<img src='cargo.png'/>

# Paciente
<img src='paciente.png'/>

# Especialidades
<img src='especialidades.png'/>

# Internação
<img src='internacao.png'/>

# Enfermeiro
<img src='enfermeiro.png'/>

# Convênio
<img src='convenio.png'/>

# Receita
<img src='receita.png'/>


# Parte 4 - Realizando alterações no banco de dados

<p> Crie um script que adicione uma coluna “em_atividade” para os médicos, indicando se ele ainda está atuando no hospital ou não. 

Crie um script para atualizar ao menos dois médicos como inativos e os demais em atividade. </p>



<img src='update.png'/>
<br>

# Parte 5 - Consultas no banco de dados

### Todos os dados e o valor médio das consultas do ano de 2020
```
SELECT AVG(valor_consulta) FROM consulta WHERE YEAR(data_consulta)=2020;
```
<img src='Parte5-1.png' align="center"/> <br><br>
### Todos os dados das internações que tiveram data de alta maior que a data prevista para a alta.
```
SELECT * FROM internacao WHERE data_alta>data_prev_alta;
```
<img src='Parte5-2.png' align="center"/> <br><br>
### Receituário completo da primeira consulta registrada com receituário associado.
```
SELECT * FROM consulta INNER JOIN receita ON consulta.receitado = receita.id_receita ORDER BY data_consulta LIMIT 1;
```
<img src='Parte5-3.png' align="center"/> <br><br>
### Todos os dados da consulta de maior valor e também da de menor valor.
```
SELECT *, MIN(valor) FROM consulta UNION ALL SELECT *, MAX(valor) FROM consulta; 
```
<img src='Parte5-4.png' align="center"/> <br><br>
### Data, procedimento e número de quarto de internações em quartos do tipo “apartamento”.
```
SELECT * FROM internacao INNER JOIN quarto ON internacao.quarto WHERE quarto.id_quarto = 1;
```
### Nome do paciente, data da consulta e especialidade de todas as consultas em que os pacientes eram menores de 18 anos na data da consulta e cuja especialidade não seja “pediatria”, ordenando por data de realização da consulta.
```
SELECT paciente.nome, paciente.ano_nascimento, consulta.data_consulta FROM paciente JOIN consulta ON paciente.cpf = consulta.cpf_paciente INNER JOIN especialidade ON especialidade.id = consulta.e_buscada WHERE consulta.e_buscada <> 1 AND YEAR(consulta.data_consulta) - YEAR(paciente.ano_nascimento) < 19 OR YEAR(consulta.data_consulta) - YEAR(paciente.ano_nascimento) > 0 ORDER BY consulta.data_consulta; 
```
<img src='Parte5-6.png' align="center"/> <br>
8-


