# Lakehouse Sísmico Europeu · EMSC no Databricks (Bronze)
1. `01_extract_EU` baixa da API FDSN do EMSC 12 arquivos mensais (M ≥ 2,5, retângulo 27–72°N e 32°W–45°E) para a landing, conferindo `/count`, janela do mês e `unid` únicos, e anota cada extração em `extracoes_manifesto`.
2. `02_bronze_EU` usa o Auto Loader para ler só arquivo novo e gravar `sismos_eu.bronze.terremotos_raw` (1 linha = 1 arquivo); a 2ª execução grava 0 linhas, e o `DESCRIBE HISTORY` prova isso.
3. Ordem: rode o 01 e depois o 02, e confira na seção 5 do 02 que `bate = true` e `repetidos = 0`; use `recomecar = sim` só se os arquivos foram reescritos e volte para `nao` em seguida.
4. Cada fonte tem o seu próprio checkpoint (nunca compartilhe com o USGS), porque ele é a memória de uma consulta só.
5. Dados: EMSC-CSEM SeismicPortal (https://www.seismicportal.eu), com crédito à fonte; Silver ainda não faz parte desta etapa.
