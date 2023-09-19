teste# COMANDO_ORACLE

COALESCE(X,1) /*"Se x for nulo, fica 1"*/
CASE WHEN XXXX > 0 THEN resposta ELSE resposta_else END nome_linha
SUM() /*' Soma '*/
MAX() /* 'Valor maior' */
MIN() /* 'Valor menor' */
UPPER() /* 'Deixa a letra maiuscula' */ 
LOWER() /* 'Deixa a letra minuscula' */
LIKE() /* 'Pesquisa palavras' */
COUNT() /* 'contar a quantidade de registro' */
LENGTH() /* 'conta caractere' */
TO_INT() /* 'Deixa o 'campo' em inteiro' */
TO_CHAR() /* 'Deixa o 'campo' em str' */
TO_CHAR(SYSDATE, 'DD/MM/YYYY') DATA /*"Formata a data em str"*/
TO_CHAR(SYSDATE, 'YYYY-MM-DD HH24:MI:SS') DATA /*"Formata a data com hora e minutos em str"*/
TO_DATE(TO_CHAR(ChequePendente.DataEmissao, 'DD/MM/YYYY'), 'DD/MM/YYYY') DataEmissao /*"Formata a data"*/
RPAD(xxx,10,' ') /*"Coloca os espaços a direita faltantes do valor 10 - x"*/
LPAD(xxx,10,' ') /*"Coloca os espaços a esquerda faltantes do valor 10 - x"*/
TRIM() /* 'Tirar os espaços' */
TRUNC() /* 'Tirar os minutos/hora' */

UNION /*"Unir SELECT com DISTINCT"*/
UNION ALL /*"Unir SELECT sem DISCTINCT"*/

SELECT DISTINCT /* 'Tras os valores sem repetir' */
SELECT /* 'Tras os valores repetindo' */

IN(1,2) /*'Apenas pegar esse valores'*/
NOT IN(1,2) /*'pegar valores diferente de'*/

EXISTS() /* 'Pegar valores q vc setar' */
NOT EXISTS() /* 'Pegar todos os valores menos os q vc setar' */

IS NULL /*'é nulo'*/
NOT NULL /*'Não é nulo'*/

ORDER BY /*'ordernar'*/

FETCH FIRST 1 ROWS ONLY /*'pega o primeiro valor'*/

GRANT SELECT,INSERT,UPDATE ON tabela TO nome_servidor; /* 'Permissao na tabela' */

SYS_CONTEXT('USERENV','CLIENT_IDENTIFIER') /* 'Pega o usuario logado no banco' */

EXTRACT(YEAR FROM campo) /* 'Pegar apenas o ano' */
EXTRACT(MONTH FROM campo) /* 'pegar apenas o mes' */
EXTRACT(DAY FROM campo) /* 'pegar apenas o dia' */

<> /* 'diferente' */
= /* 'igual' */

-------------------------
INSERT INTO tabela(seq,nome,descricao)
   VALUES(:PAR_SEQUENCIA, :PAR_NOME, :PAR_DESCRICAO)

-------------------------
DELETE FROM tabela
   WHERE nome = :par_NOME
   
-------------------------
UPDATE tabela
SET nome_campo = 'test'
WHERE 
   C.SEQUENCIA = :PAR_SEQUENCIA 
   AND C.ATIVO = 'N'
   
-------------------------
/*'selecionar o proximo valor de uma sequence'*/
SELECT 
  SELETIVODBA.SEQ_VOUCHER.NEXTVAL 
FROM
  DUAL;
  
-------------------------
/*'Alterar o valor da sequence usando o "-" voce diminui o valor, usando o "+" voce sobe o valor'*/
ALTER SEQUENCE S_SEG_EXE INCREMENT BY 1

-------------------------
/*'usar na multi-select'*/
AND TO_CHAR(HF.CODTIPOFINANCEIRO) IN (  
             SELECT
                 regexp_substr(COALESCE(:PAR_CODTIPOFINANCEIRO, TO_CHAR(HF.CODTIPOFINANCEIRO)), '[^,]+', 1, LEVEL)
        	 FROM
                 DUAL
             CONNECT BY
              	regexp_substr(COALESCE(:PAR_CODTIPOFINANCEIRO, TO_CHAR(HF.CODTIPOFINANCEIRO)), '[^,]+', 1, LEVEL) IS NOT NULL)
	       
-------------------------
/*'guarda o select em uma variavel'*/
WITH TDATA as (
  SELECT NOME,CIDADE,ANO
  FROM ALUNO A
  WHERE A.NOME = 'DIEGO'
)
SELECT *
FROM ( 
      SELECT 1 ORDEM
      FROM TDATA
      UNION
      SELECT 2 ORDEM
      FROM TDATA
)
ORDER BY ORDEM

-------------------------
/* 'Cria uma tabela ficticia para rodar o SELECT ' */
SELECT
	TO_CHAR(SYSDATE, 'DD/MM/YYYY HH24:MI:SS') DATETIME
FROM DUAL

-------------------------
/* 'Adicionar FOREIGN KEY' */
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
   FOREIGN KEY (column1, column2, ... column_n)
   REFERENCES parent_table (column1, column2, ... column_n);
