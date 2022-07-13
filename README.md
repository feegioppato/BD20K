# 20 cidades que desmataram mais que 20.000 campos de futebol nos últimos 20 anos

Dificuldade: Alta
Esfera: Pessoal
Feito: Yes
Prioridade: Baixa

[READ.md](https://www.notion.so/READ-md-d955e045ced246bc9d9fa688a58e03a8)

### Query tweet BD20K

```sql
WITH desmat as (
  SELECT id_municipio, MAX(area) as area_total
  FROM `basedosdados.br_mapbiomas_estatisticas.transicao_municipio_de_para_anual`
  WHERE ano BETWEEN 1999 AND 2019
    AND de_nivel_2 = "1.1. floresta natural"
    AND para_nivel_1 = "3. agropecuaria"
    AND area > 16210
  GROUP BY id_municipio
  )

SELECT t1.sigla_uf, t1.nome, t2.ano, desmat.id_municipio, desmat.area_total
FROM desmat
INNER JOIN `basedosdados.br_bd_diretorios_brasil.municipio` AS t1
ON desmat.id_municipio = t1.id_municipio
INNER JOIN `basedosdados.br_mapbiomas_estatisticas.transicao_municipio_de_para_anual` as t2
ON desmat.area_total = t2.area
ORDER BY desmat.area_total DESC
LIMIT 20
```

### Query tweet BD20K - Mapa

```sql
WITH desmat as (
  SELECT id_municipio, MAX(area) as area_total
  FROM `basedosdados.br_mapbiomas_estatisticas.transicao_municipio_de_para_anual`
  WHERE ano BETWEEN 1999 AND 2019
    AND de_nivel_2 = "1.1. floresta natural"
    AND para_nivel_1 = "3. agropecuaria"
    AND area > 16210
  GROUP BY id_municipio
  )

SELECT t1.sigla_uf, t1.nome, t2.ano, desmat.id_municipio, desmat.area_total
FROM desmat
INNER JOIN `basedosdados.br_bd_diretorios_brasil.municipio` AS t1
ON desmat.id_municipio = t1.id_municipio
INNER JOIN `basedosdados.br_mapbiomas_estatisticas.transicao_municipio_de_para_anual` as t2
ON desmat.area_total = t2.area
ORDER BY desmat.area_total DESC

```