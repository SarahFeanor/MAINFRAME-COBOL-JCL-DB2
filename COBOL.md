# ⚡COBOL

 - Referências e Exemplos de código em COBOL

## 1. A Instrução MOVE:

- DECLARAÇÃO DE MOVIMENTAÇÃO 

- TIPO DE DADO DE A
```COBOL
Tipo A               Valor de A	
PIC 99V99	    12.35	
PIC 99V99	    12.35	
PIC 99V999	    12.345	
PIC9(05)V9(03)	    54321.543	
PIC 9(04)V9(02)	    23.24	
PIC 99V99	    00.34	
PIC X(04)	    MUSA	
```
- TIPO DE DADO DE B
```COBOL
Tipo B 	          Valor de B após o movimento
PIC 999V99	  012.35
PIC 9999V9999	  0012.3500
PIC 9V99	  2.34
PIC 9(03)V9(03)	  321.543
PIC ZZZ99.9	  23.2
PIC $$$.99	  $.34
XBXBXB	          M U S
```
## 2. Cláusula SYNC:
```COBOL
  01 MEUS-DADOS.
     05 DATA-ONE PIC X(6).
     05 DADOS-DOIS PIC 9(6) COMP SYNC.
     05 DADOS-TRES PIC S9(4)V99 COMP-3.
```
## 3. A Instrução REDEFINES:
```COBOL
  01 WS-DATA PIC 9(06).
  01 WS-REDEF-DATE REDEFINES WS-DATE.
     05 WS-ANO ​​PIC 9(02).
     05 WS-MES PIC 9(02).
     05 WS-DAY PIC 9(02).
 ```
 
## 4. A Instrução RENAMES:
```COBOL
  01 WS-REPSONSE.
     05 WS-CHAR143 PIC X(03).
     05 WS-CHAR4 PIC X(04).
     66 ADD-REPSONSE RENAMES WS-CHAR143.
 ```
 
## 5. O Nível 88 como condição de Validação de opções:
```COBOL
  01 GENERO PIC X.
     88 MASCULINO VALUE '1'
     88 FEMININO  VALUE '2' '3'.
 ``` 
## 6. Operação aritmética - Adicionar (ADD):
```COBOL

Operação ADD	            A	B	C	D
--------------------------------------------------------
ADD A TO B	            A	A+B
--------------------------------------------------------
ADD A B C TO D	            A	B	C	A+B+C+D
--------------------------------------------------------
ADD A B C GIVING D	    A	B	C	A+B+C
--------------------------------------------------------
ADD A TO B C	            A	A+B	A+C	
--------------------------------------------------------
```
## 7. Operação Aritmética - Subtrair (SUBTRACT):
```COBOL
Operação SUBTRACT	        A	B	C	D
------------------------------------------------------------
SUBTRACT A FROM B	        A	B-A
------------------------------------------------------------
SUBTRACT A B FROM C	        A	B	C-(A+B)
------------------------------------------------------------
SUBTRACT A B FROM C GIVING D	A	B	C	C-(A+B)
------------------------------------------------------------

```
## 8. Operação aritmética - Multiplicar (MULTIPLY):
```COBOL

Operação MULTIPLY	        A	B	C	D
------------------------------------------------------------
MULTIPLY A BY B	                A	A*B		
------------------------------------------------------------
MULTIPLY A BY B GIVING C	A	B	A*B	
------------------------------------------------------------
```
## 9. Operação Aritmética - Dividir (DIVIDE):
```COBOL
Operação DIVIDE	                        A	  B	C	      D
-----------------------------------------------------------------------------------
DIVIDE A INTO B	                        A	  B/A	
-----------------------------------------------------------------------------------
DIVIDE A INTO B GIVING C	        A	  B	B/A	
-----------------------------------------------------------------------------------
DIVIDE A BY B GIVING C	                A	  B	A/B	
-----------------------------------------------------------------------------------
DIVIDE A INTO B GIVING C REMAINDER D    A	  B	Inteiro(B/A)	Restante inteiro
-----------------------------------------------------------------------------------
```

## 10. O GIVING em operadores aritiméticos:
```COBOL
Operação Aritmética	               A	 B	C	       D
-----------------------------------------------------------------------------------
ADD A B C GIVING D	               A	 B	C	       A+B+C
-----------------------------------------------------------------------------------
SUBTRACT A B FROM C GIVING D	       A	 B	C	       C-(A+B)
-----------------------------------------------------------------------------------
MULTIPLY A BY B GIVING C	       A	 B	A*B	
-----------------------------------------------------------------------------------
DIVIDE A INTO B GIVING C REMAINDER D   A	 B	Inteiro(B/A)	Restante inteiro
-----------------------------------------------------------------------------------
```

## 11. A Instrução CORRESPONDING (CORR)
```COBOL
  05 WS-CAMPO-1.
     10 WS-FIELD-A PIC S9(3).
     10 WS-CAMPO-B PIC +99,9.
     10 WS-FIELD-C PIC X(4).
     10 WS-FIELD-D REDEFINES WS-FIELD-C PIC 9(4).
     10 WS-FIELD-E USAGE COMP-1.
     10 WS-FIELD-F USAGE INDEX.
 
  05 WS-CAMPO-2.
     10 WS-FIELD-A PIC 99.
     10 WS-CAMPO-B PIC +9V9.
     10 WS-FIELD-C PIC A(4).
     10 WS-FIELD-D PIC 9(4).
     10 WS-FIELD-E PIC 9(9) COMP.
     10 WS-FIELD-F USAGE INDEX..
```
> Se a instrução ADD CORR WS-FIELD-2 TO WS-FIELD-1 for especificada, ocorrerá uma soma entre os campos correspondentes. Os campos correspondentes são WS-FIELD-A e WS-FIELD-A, WS-FIELD-B e WS-FIELD-B, e WS-FIELD-E e WS-FIELD-E.

> No entanto, alguns campos não são incluídos na soma. O campo WS-FIELD-C não é incluído porque não é um campo numérico. O campo WS-FIELD-D também não é incluído porque possui uma cláusula REDEFINES em sua descrição de dados, o que indica que ele está sendo redefinido e não é tratado como um campo separado para fins de soma.

> Além disso, o campo WS-FIELD-F não é incluído porque é um item de dados de índice, o que significa que é usado para acessar ou identificar registros em uma estrutura de dados, mas não contém um valor numérico para ser somado.

> Portanto, ao executar a instrução ADD CORR WS-FIELD-2 TO WS-FIELD-1, apenas os campos correspondentes que são numéricos e não possuem redefinições são considerados na soma. Os demais campos não são afetados pela operação de adição.


## 12. Declaração PERFORM simples
```COBOL
  PERFORM PARAGRAFO-X.
```
  
- A instrução PERFORM transfere o controle para o "PARAGRAFO-X", após a execução do parágrafo "PARAGRAFO-X", o controle retorna para a próxima instrução de PERFORM e continua a execução.

- Nota: A forma simples do PERFORM atua de forma muito semelhante à instrução GO TO, exceto que após a execução do controle de parágrafo ele retornará de onde foi chamado.

## 13. A declaração PERFORM composta
```COBOL   
   PERFORM PARAGRAFO-X UNTIL PARAGRAFO-Y
```
  
"PARAGRAFO-X" e "PARAGRAFO-Y" são nomes de parágrafos. 

- A execução da instrução PERFORM faz a transferências de controle para o primeiro parágrafo "PARAGRAFO-X". Ele executa todas as instruções do primeiro paragrafo "PARAGRAFO-X" e continua até executar também todas as instruções do ultimo parágrafo na declaração, no exemplo, é o "PARAGRAFO-Y" e após executar tudo no range entre esses dois parágrafos, o controle retorna para a próxima instrução executável após essa declaração PERFORM. 

Se houver quaisquer outros parágrafos entre "PARAGRAFO-X" e "PARAGRAFO-Y", todas aquelas instruções serão executadas.

## 14. Usando PERFORM com TIMES
```COBOL
  PERFORM PARAGRAFO-X UNTIL PARAGRAFO-Y 5 TIMES.
```

- Todas as instruções no escopo (tudo que houver) do "PARAGRAFO-X" até "PARAGRAFO-Y" serão executados 5 vezes. Após esse range ser executado 5 vezes (conforme esse exemplo), o controle então passa para a próxima instrução executável após a instrução PERFORM.

## 15. A declaração PERFORM com VARYING
```COBOL
  PERFORM PARAGRAFO-X VARYING WS-A FROM 1 BY 1 UNTIL WS-A > 5
``` 
Todas as instruções no parágrafo "PARAGRAFO-X" serão executadas até a codição associada a UNTIL for atendida (verdadeira). 

- Para a primeira iteração, WS-A vale 1 (como é especificado após o FROM), para a segunda iteração, o valor WS-A aumenta em 1 (conforme especificado após a palavra-chave BY - é feito um incremento sequencia de 1 em 1) e será testado e caso a condição ainda não seja atendida, a execução se repete executando o conteúdo no "PARAGRAFO-X" e segue a incrementação em WS-A até que a condição seja satisfatóriamente atendida (verdadeira). 

- Esse é uma condição simples de loop, o qual a condição mantém a execução do "PARAGRAFO-X" enquanto for falsa, incrementando 1 à variável WS-A e testando, repetindo esse processo continuamente, até a condiçao ser plemanete atendida (verdadeira - quiando Este loop continua até que a condição se torne verdadeira, ou seja, neste exemplo, quando WS-A for maior que 5.

## 16. A declaração PERFORM com VARYING e AFTER
```COBOL
    PERFORM PARAGRAFO-X VARYING WS-A FROM 1 BY 1 UNTIL WS-A > 10
      AFTER WS-B FROM 1 BY 1 UNTIL WS-B > 5
 ``` 
- Neste exemplo, além de WS-A, o valor de WS-B também é alterado. Um exemplo típico de Matriz ou de Array. Para cada valor válido em WS-A, o valor de WS-B começa de 1 até que a condição de WS-B > 5 seja verdadeira. A execução da instrução PERFORM termina somente quando WS-A for > 10.

## 17. Instrução Condicional - IF (se) Simples
```COBOL
  IF (alguma coisa)
      {faça algo aqui, caso a condição acima seja atendida}
  [END-IF].
```  
- Se a condição for verdadeira, ele executará o conjunto de instruções escritas no bloco IF. Se a condição não for satisfeita, o controle será transferido para as próximas instruções após o término da instrução IF.

- END-IF é o terminador de escopo, que é opcional no programa. O ponto (.) pode ser definido na última instrução do bloco IF. Se não especificarmos o período, o terminador de escopo END-IF é obrigatório.

## 18. Declaração Condicional ELSE (se não)
```COBOL    
    SE Condição-1
        {Statement-Block-1}
    [ELSE]
        {Declaração-Bloco-2}
    [END-IF].
```

- Em IF-ELSE, o bloco de instruções será executado se a condição especificada for verdadeira. Se a condição for falsa, o outro conjunto de instruções será executado, e esses conjuntos estarão sob o bloco ELSE.

## 19. Instrução condicional IF aninhado
```COBOL
 IF Condição-1 THEN
        IF Condição-2 THEN
            Declarações-bloco-1
        ELSE
            Declarações-bloco-2
        END-IF
    ELSE
        IF Condição-3 THEN
            Declarações-bloco-3
        ELSE
            Declarações-bloco-4
        END-IF
    END-IF.
  ```
- Uma chamada de instrução IF aninhada é uma cadeia de instrução IF dentro de outra(s) instrução(ões) IF.

## 20. Declaração EVALUATE simples
```COBOL
  EVALUATE WS-DATA-TYPE-IND
      WHEN A
           DISPLAY 'Letra A'
      WHEN '1'
           DISPLAY 'Número 1'
      WHEN 'X'
           DISPLAY 'Letra X'
      WHEN OTHER
           DISPLAY 'Qualquer outro valor'
  END-EVALUATE
 ```
- Este exemplo avalia WS-DATA-TYPE-IND, se WS-DATA-TYPE-IND for 'A' é exibido 'Letra A', se WS-DATA-TYPE-IND for '1' exibe 'Numero 1', se WS-DATA-TYPE-IND for 'X' exibirá 'Letra X'. Se a variável WS-DATA-TYPE-IND não for 'A' ou '1' ou 'X', então exibe 'Qualquer outro valor'.

## 21. A declaração EVALUATE com ALSO
```COBOL
  EVALUATE TRUE ALSO WS-SEXO ALSO WS-IDADE
        WHEN WS-SALARIO >= 1000 AND < 50000 ALSO 'M' ALSO 25 THRU 50
            MOVE 0.5 TO WS-TAX-IMP
        WHEN WS-SALÁRIO >= 1000 E < 50000 ALSO 'F' ALSO 25 THRU 60
            MOVE 0.25 TO WS-TAX-IMP
        WHEN OTHER
            MOVE 0 TO WS-TAX-IMP
    END-AVALUATE.
```  
- Este exemplo é um exemplo de tabela de decisão, calcula a taxa de imposto com base em renda, idade e sexo. A primeira cláusula WHEN satisfará se a condição de renda (>= 1.000 e < 50.000) é verdadeira, o sexo é 'M' e a idade está na faixa de 25 a 50, se for verdade, então a excuta a instrução MOVE e o controle sai de EVALUATE.

- Se a primeira condição WHEN se tornar falsa, então o controle vai para a segunda condição WHEN e verifica a condição, se é verdadeira ou falsa, se for verdadeira, ele executará a instrução MOVE após a segunda condição WHEN. Se a segunda condição WHEN for falsa, então o controle irá para a instrução MOVE codificada após o WHEN OTHER, aqui ele não verificará se é verdadeiro ou falso.

22. Declaração STRING
```COBOL
  STRING WS-NOME DELIMITED BY " "
          " " DELIMITED BY SIZE
          WS-SOBRENOME DELIMITED BY " "
       INTO WS-NOME-COMPLETO.
 ```
 
Nome do campo - Valor

WS-NOME: SARAH

WS-SOBRENOME: REZENDE

WS-NOME-COMPLETO: SARAH REZENDE



## 23. Declaração UNSTRING
```COBOL
  UNSTRING WS-NOME-COMPLETO
          DELIMITED BY " "
      INTO WS-NOME
           WS-SOBRENOME.
```
  
Nome do campo	| Valor

WS-NOME-COMPLETO: SARAH REZENDE

WS-NOME:	SARAH

WS-SOBRENOME:	REZENDE


## 24. Declaração INSPECT com opção TALLYING
```COBOL
  INSPECT WS-STRING TALLYING WS-COUNT TO CHARACTER.
``` 
Nome do campo	| Valor

WS-STRING: SARAHREZENDE

WS-COUNT	12

```COBOL
  INSPECT WS-STRING TALLYING WS-COUNT FOR ALL 'A'.
``` 
Nome do campo	| Valor

WS-STRING: SARAH REZENDE

WS-COUNT:	2

## 25. Instrução INSPECT com opção REPLACING

```COBOL
  INSPECT WS-STRING REPLACING ALL 'A' BY 'I'.
```
Nome do campo	| Valor

WS-STRING antes:	SARAH REZENDE

WS-STRING depoiS: SIRIH REZENDE

## 26. Modificação de referência na declaração MOVE
```COBOL
  MOVE WS-NOME-COMPLETO(1:5) TO WS-NOME
```
  
Nome do campo	| Valor

WS-NOME-COMPLETO:	SARAH REZENDE

WS-NOME: SARAH

```COBOL
  MOVE WS-CELULAR PARA WS-DDD(1:3)
```  
Nome do campo	| Valor

WS-CELULAR: 031997827424

WS-DDD: 031
