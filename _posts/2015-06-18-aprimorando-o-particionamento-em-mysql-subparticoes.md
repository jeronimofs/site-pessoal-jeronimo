---
layout: post
title: "Aprimorando o particionamento em MySQL – Subpartições"
---
Dando seguimento ao [post anterior sobre particionamento de tabelas no MySQL](https://jeronimo.dev.br/acelerando-suas-queries-com-o-particionamento-do-mysql/), este post explica um passo a mais: subparticionamento.

O MySQL permite que você particione uma partição, onde o primeiro nível (PARTITION) é definido por uma expressão de particionamento, e o nível inferior (SUBPARTITION) é definido por outra.

Para utilizar o subparticionamento, é necessário seguir duas restrições:

- O tipo de particionamento (PARTITION) precisa ser dos tipos RANGE ou LIST;
- O tipo de particionamento (SUBPARTITION) precisa ser dos tipos HASH ou INDEX. Portanto, não é possível subparticionar tabelas particionadas por HASH ou INDEX.

É importante notar que o número total de partições de uma tabela (nº de PARTITIONs * nº de SUBPARTITIONs) não pode ultrapassar 1024, que é o máximo que o MySQL suporta. Ex.: se uma tabela é particionada por RANGE em 2 partições, cada partição pode ser subparticionada em 512, pois 2 * 512 = 1024.

Abaixo segue um exemplo de tabela subparticionada:

```sql
CREATE TABLE ts ( 
    id INT, 
    purchased DATE 
) PARTITION BY RANGE( YEAR(purchased) ) 
SUBPARTITION BY HASH( TO_DAYS(purchased) ) 
SUBPARTITIONS 2 ( 
    PARTITION p0 VALUES LESS THAN (1990), 
    PARTITION p1 VALUES LESS THAN (2000), 
    PARTITION p2 VALUES LESS THAN MAXVALUE 
); 

```

No exemplo acima a tabela ts possui 3 partições, e cada uma é subparticionada em 2 partições. Assim, temos 6 partições no total.

Veja outro exemplo:

```sql
CREATE TABLE ts ( 
    id INT, 
    purchased DATE 
) PARTITION BY RANGE( YEAR(purchased) ) 
SUBPARTITION BY HASH( TO_DAYS(purchased) ) ( 
    PARTITION p0 VALUES LESS THAN (1990) ( 
        SUBPARTITION s0, 
        SUBPARTITION s1 
    ), 
    PARTITION p1 VALUES LESS THAN (2000) ( 
        SUBPARTITION s2 
    ), 
    PARTITION p2 VALUES LESS THAN MAXVALUE ( 
        SUBPARTITION s3, 
        SUBPARTITION s4 
    ) 
); 

```

Neste outro exemplo, a tabela ts tem 5 partições no total, pois as partições p0 e p2 são subparticionadas em 2 partições cada, mas a partição p1 tem apenas uma subpartição.

Para saber mais sobre o subparticionamento em MySQL, consulte [a documentação oficial do MySQL sobre subparticionamento](https://dev.mysql.com/doc/refman/5.7/en/partitioning-subpartitions.html).