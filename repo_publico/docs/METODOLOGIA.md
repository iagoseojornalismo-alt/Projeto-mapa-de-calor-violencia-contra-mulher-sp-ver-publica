# Metodologia

## Fonte dos dados

Os dados têm origem em pedido via **Lei de Acesso à Informação (LAI)** à **Secretaria de Segurança Pública do Estado de São Paulo (SSP-SP)**, protocolo FALASP. Duas bases foram fornecidas, ambas extraídas do sistema de **Registro Digital de Ocorrências (R.D.O.)**:

| Base | Fonte (sistema) | Recorte | Período | Linhas |
|---|---|---|---|---|
| Feminicídio e tentativa | SPVida | Homicídio doloso / tentativa, detalhamento Feminicídio / Feminicídio tentado. Tipo de pessoa: vítima. Por **data de ocorrência**. | 01/01/2025 a 30/04/2026 | 1.415 |
| Violência doméstica | SPJ (Sistema de Polícia Judiciária) | Rubrica "Violência Doméstica". Por **data de registro**. | 01/01/2025 a 30/04/2026 | 270.295 |

## Observações da SSP sobre os dados (resumo)

A SSP anexou ao pedido uma nota metodológica com os seguintes pontos, que orientam toda a leitura deste material:

1. O R.D.O. é a ferramenta de registro dos boletins de ocorrência. Sua implantação foi gradual; **abrangência plena de todos os municípios só a partir de 2010**. Campos e tabelas estão em constante aperfeiçoamento.
2. A inclusão/alteração de campos ao longo do tempo pode afetar critérios de pesquisa — **não há tratamento metodológico que qualifique esta base como estatística oficial**.
3. A data de extração pode alterar o resultado: **o cidadão pode registrar o fato a qualquer momento**, não necessariamente no dia, mês ou ano em que ocorreu.
4. O número de boletins **não equivale à estatística criminal do Estado**. A estatística oficial segue a Resolução SSP nº 160/01, consultável em ssp.sp.gov.br.
5. Cada linha da base corresponde a uma pessoa/natureza/objeto do boletim — um mesmo B.O. pode gerar várias linhas. Para contagem de **ocorrências** (não linhas), a SSP orienta deduplicar por `NOME_DELEGACIA + ANO_BO + NUM_BO`.
6. Cerca de **60% dos registros são feitos fora do município onde o fato ocorreu** (o cidadão pode registrar em qualquer delegacia do Estado).
7. Campos que poderiam identificar pessoas são protegidos pelo **art. 31 da Lei de Acesso à Informação** (Lei 12.527/2011).
8. Os **históricos dos boletins não foram disponibilizados** (haveria necessidade de pedido específico, vinculado a uma das hipóteses do §3º do art. 31 da LAI).

O dicionário de campos completo, fornecido pela SSP, está em [`DICIONARIO_DADOS.md`](./DICIONARIO_DADOS.md).

## Decisões editoriais e de tratamento de dados

### 1. Data de registro × data do fato
A base de violência doméstica é organizada por **data de registro do B.O.**, não data do fato. Como o registro pode ocorrer a qualquer momento, parte das ocorrências registradas no período (jan/2025–abr/2026) refere-se a fatos ocorridos antes — em alguns casos, anos antes. O mapa e o infográfico deixam essa distinção explícita em nota, para que o leitor não confunda "quando foi comunicado" com "quando aconteceu".

### 2. Geolocalização
- Cada ocorrência tem cidade e bairro declarados no B.O. Os bairros foram geocodificados (Nominatim/OpenStreetMap) e posicionados pelo **centro médio** das ocorrências daquele bairro — não há exibição de endereço individual.
- **92,2%** das ocorrências têm bairro geolocalizado (24.011 pares cidade+bairro distintos, em 645 municípios).
- Bairros sem coordenada própria são posicionados no **centro do respectivo município** (posição aproximada, não exata) — mecanismo que cobre a maior parte do restante.
- No total, **99,998%** das ocorrências aparecem no mapa. O resíduo irredutível (6 ocorrências, 0,002%) tem cidade de registro fora do Estado de São Paulo (ex.: registros com cidade "Brasília", "Niterói", localidades de Minas Gerais, ou "outro país") e por isso não há território estadual onde posicioná-lo — esses casos permanecem nos totais gerais, mas não no mapa.

### 3. "Área rural" — dispersão em vez de ponto único
Cerca de 2% das ocorrências têm o bairro registrado de forma genérica como "Rural" / "Área Rural" / "Zona Rural", sem endereço mais específico. Concentrar esses casos num único ponto geográfico (o que a geolocalização ingênua faria) cria **focos de calor artificiais** — um ponto só, por exemplo, concentrando os ~1.176 casos rurais de Franca. Para evitar essa distorção:
- Esses pontos foram **redistribuídos** (técnica de *dot-density*, com posições aleatórias reproduzíveis — semente fixa) dentro do polígono do respectivo município (limites do IBGE), preservando exatamente o total de casos por categoria.
- Saíram do ranking de "bairros com mais ocorrências" (não são um bairro específico).
- A nota do mapa informa esse tratamento.

### 4. Auditoria e conciliação de totais
Antes da publicação, foi feita uma auditoria comparando, linha a linha, os totais declarados contra a soma efetiva dos pontos plotados no mapa. Foram encontradas e corrigidas duas falhas pontuais de correspondência de nomes de município (acentuação/apóstrofo) que faziam 109 ocorrências de violência doméstica e 1 feminicídio não aparecerem em lugar nenhum do mapa, apesar de contabilizados no total. O detalhamento completo está em [`AUDITORIA.md`](./AUDITORIA.md).

## Limitações conhecidas

- Não há informações de raça/cor, idade ou perfil da vítima na base de violência doméstica (apenas na de feminicídio/tentativa).
- Não há campo de escolaridade em nenhuma das duas bases.
- A base não constitui estatística criminal oficial (ver item 4 acima).
- Cerca de 60% dos registros podem ter sido feitos em delegacia diferente da circunscrição do fato.
