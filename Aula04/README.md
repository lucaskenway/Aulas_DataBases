Lab 01: Explorando Dados com SQL

Objetivo:
Aprender a extrair informações estratégicas de um banco de dados já existente.

Passo 1: Preparando o Terreno
Copie e cole o conteúdo do arquivo setup_(mysql/postgres).sql (disponível no repositório) no seu editor SQL e execute tudo. Isso criará as tabelas de Médicos, Pacientes e Consultas com dados fictícios para trabalharmos.

Desafios (TF)
Escreva as consultas SQL para responder às seguintes perguntas de negócio:

Lista de Contatos: Precisamos de uma lista com o nome de todos os pacientes e seus respectivos telefones, ordenados alfabeticamente.

Faturamento Total: Qual o valor total arrecadado pela clínica até hoje?

Agenda do Dia: Liste o nome do paciente, o nome do médico e a hora da consulta para todos os atendimentos. (Dica: Você precisará de 2 JOINs).

Pacientes Ausentes: Liste o nome de todos os pacientes cadastrados que ainda não realizaram nenhuma consulta. (Dica: Use LEFT JOIN e procure por NULL).

Especialidades Populares: Qual a especialidade médica que mais realizou consultas na clínica?

Entrega:
Suba um arquivo chamado respostas.sql no seu GitHub contendo as 5 queries numeradas.