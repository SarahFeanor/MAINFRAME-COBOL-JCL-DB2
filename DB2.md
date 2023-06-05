# ⚡DB2

 - Referências e Exemplos de códigos SQL no DB2

## 1. SQL SELECT - Busca coluna(s) específica(s) de uma tabela
```SQL
SELECT nome_da_coluna1, nome_da_coluna2, ... FROM nome_da_tabela;
```
## 2. SQL SELECT - Busca todas as colunas de uma tabela
```SQL
SELECT * FROM nome_da_tabela;
```
## 3. SELECT DISTINCT - Seleciona apenas os valores da coluna DISTINCT da tabela.
```SQL
SELECT DISTINCT nome_da_coluna1 FROM nome_da_tabela;
```
## 4. SELECT COUNT(DISTINCT) - lista o número de valores diferentes (distintos) na coluna da tabela.
```SQL
SELECT COUNT(DISTINCT column_name) FROM nome_da_tabela;
```
## 5. WHERE - Busca registros com base no(s) campo(s) de texto na cláusula where
```SQL
SELECT * FROM nome_da_tabela WHERE column_name='text_value';
```
## 6. WHERE - Busca registros com base em campos numéricos na cláusula where
```SQL
SELECT * FROM nome_da_tabela WHERE nome_da_coluna=valor_numérico;
```
## 7. Operador AND na cláusula WHERE
```SQL
SELECT * FROM nome_da_tabela WHERE nome_da_coluna1=valor_numérico AND nome_da_coluna2=valor_numérico;
```
## 8. Operador OR na cláusula WHERE
```SQL
SELECT * FROM nome_da_tabela WHERE nome_da_coluna1=valor_numérico OR nome_da_coluna2=valor_numérico;
```
## 9. Operador NOT na cláusula WHERE
```SQL
SELECT * FROM nome_da_tabela WHERE NOT nome_da_coluna=valor_numérico;
```
## 10. Operador AND/OR na cláusula WHERE
```SQL
SELECT * FROM nome_da_tabela WHERE nome_da_coluna1=valor_numérico1 AND (column_name2=numeric_value2 OR column_name3=numeric_value3);
```
## 11. ORDER BY - Ordenar o registro em ordem crescente
```SQL
SELECT * FROM nome_da_tabela ORDER BY nome_da_coluna;
```
## 12. ORDER BY - Ordenar o registro em ordem decrescente
```SQL
SELECT * FROM nome_da_tabela ORDER BY nome_da_coluna DESC;
```
## 13. ORDER BY - Ordenar o registro em ordem crescente por várias colunas
```SQL
SELECT * FROM nome_da_tabela ORDER BY nome_da_coluna1, nome_da_coluna2;
```
## 14. ORDER BY - Classifica o registro em ordem decrescente por várias colunas
```SQL
SELECT * FROM nome_da_tabela ORDER BY nome_da_coluna1 DESC, column_name2 DESC;
```
## 15. INSERT INTO - Insere dados em todas as colunas em uma linha
```SQL
INSERT INTO table_name VALUES ('text_value1','text_value2',numeric_value,'text_value3');
```
## 16. INSERT INTO - Insira dados em uma coluna específica em uma linha
```SQL
INSERT INTO table_name (column_name1, column_name2, column_name3) VALUES (valor_numérico1, valor_numérico2, 'valor_texto3');
```
## 17. IS NULL - Busca linhas de coluna nulas em uma tabela
```SQL
SELECT * FROM nome_da_tabela WHERE nome_da_coluna IS NULL;
```
## 18. IS NOT NULL - Busca linhas de coluna não nulas em uma tabela
```SQL
SELECT * FROM nome_da_tabela WHERE nome_da_coluna IS NOT NULL;
```
## 19. UPDATE - Atualize uma ou várias linhas em uma tabela usando a cláusula where
```SQL
UPDATE nome_da_tabela SET nome_da_coluna1=valor1, nome_da_coluna2=valor2 WHERE nome_da_coluna=valor;
```
## 20. UPDATE - Atualizar todas as linhas em uma tabela
```SQL
UPDATE nome_da_tabela SET nome_da_coluna=valor;
```
## 21. DELETE - Excluir uma ou várias linhas em uma tabela
```SQL
DELETE FROM table_name WHERE column_name='text_value';
```
## 22. DELETE - Excluir todas as linhas em uma tabela
```SQL
DELETE FROM nome_da_tabela;
```
