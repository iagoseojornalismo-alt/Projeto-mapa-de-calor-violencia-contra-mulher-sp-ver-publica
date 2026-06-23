# Mapa-de-calor-violencia-contra-mulher-sp-vPublica

_!!!!!IMPORTANTE!!!!!!!!_

_ESTÁ VETADO O USO COMERCIAL DESSE MAPA, BEM COMO INCORPORAÇÕES DO HTML SEM AUTORIZAÇÃO PRÉVIA_

_Uma versão com licenciamento comercial está em desenvolvimento, utilizando uma base cartográfica contratada especificamente para aplicações profissionais e empresariais._

_Veículos de imprensa por assinatura, organizações e instituições interessadas em licenciamento, parcerias ou acesso antecipado podem entrar em contato diretamente comigo. Estou à disposição pelo e-mail: iagoseojornalismo@gmail.com_

_Atenciosamente,_
_Iago Y. Seo_
________________________________________
ESPECIFICAÇÕES SOBRE O MAPA DA VIOLÊNCIA CONTRA A MULHER NO ESTADO DE SÃO PAULO

Produtos: mapa de calor interativo + infográfico editorial (HTML autossuficientes) 

Fonte: Secretaria da Segurança Pública de São Paulo (SSP SP), pedido FALASP via Lei de Acesso à Informação / Recorte: 01/01/2025 a 30/04/2026 / Jornalista: Iago Yoshimi A. Seo · © 2026

*OBS: CASO HAJA O  INTERESSE PELAS PLANILHAS DE DADOS, FAVOR ENTRAR EM CONTATO NO E-MAIL: iagoseojornalismo@gmail.com*
Devido ao tamanho do arquivo, não foi possível agregar ao repositório.
________________________________________
1. Visão geral
O projeto transforma os microdados brutos da SSP SP em duas peças de leitura pública, ambas em arquivo HTML único e offline (sem conexão a banco externo em tempo de execução):
•	Mapa (mapa_violencia_mulher_sp.html): mapa de calor por bairro, em estética escura, com filtros por tipo de ocorrência, busca, ranking de bairros, limites municipais e pop-ups sem endereços individuais. Traz o infográfico embutido numa aba lateral isolada.
•	Infográfico (infografico_violencia_mulher_sp.html): peça editorial com KPIs, faixa etária, cor/raça, local, evolução mensal, horário e violência via internet.

2. Fonte e recorte dos dados
A planilha tem duas bases, com metodologias diferentes definidas pela própria SSP:

Base	Conteúdo	Linhas	Fonte SSP	Critério de período
Base 1	Feminicídio consumado e tentado (vítima)	1.415	SPVida	por ocorrência, 01/01/2025–30/04/2026
Base 2	Violência doméstica	270.295	SPJ	por data de registro, 01/01/2025–30/04/2026

A Base 1 corresponde a Homicídio doloso / Tentativa de homicídio com detalhamento Feminicídio / Feminicídio tentado. A Base 2 é integralmente rubricada como Violência Doméstica.




3. Números principais
Indicador	Total
Violência doméstica (registros)	270.295
Feminicídios consumados	374
Tentativas de feminicídio	1.041
Total de feminicídio (consumados + tentativas)	1.415

4. Datas: registro × comunicação × ocorrência
Com relação ao ponto metodológico central, a Base 2 foi extraída por data de registro. No entanto, segundo notas metodológicas da SSP, o fato pode ter ocorrido muito antes — o cidadão pode registrar a qualquer momento, o que colocou os dados diante de algumas nuances temporais anacrônicas. Na tabela abaixo distinguimos a data da ocorrência em algumas linhas.

Ano	Data de registro (critério SSP)	Data de comunicação	Data de ocorrência (fato)

2005–2023	0	1	1.187

2024	0	67	3.554

2025	194.753	194.797	193.986

2026	75.542	75.430	71.568

Pela data de registro das ocorrências (o critério oficial), a base é estritamente 2025–2026 — não há registros anteriores. Contudo, os ~4.741 fatos com data de ocorrência anterior a 2025 (sendo 1.187 antes de 2024 e 3.554 em 2024) são fatos antigos comunicados recentemente, não registros de anos passados.
Diante dessa controvérsia temporal, a decisão metodológica para a geração do mapa foi de manter o recorte por registro (fiel à SSP) e não descartamos nenhum registro — a alternativa de filtrar por data de ocorrência distorceria a série (anos antigos ficariam gravemente incompletos) e divergiria da metodologia. 
A diferença é explicada em nota de rodapé no mapa. A data fim exibida foi corrigida para 30/04/2026 (fim do período de registro); 




5. Geocodificação e cobertura

Nos microdados, apenas ~29% (Base 1) e ~29% (Base 2) das ocorrências tinham coordenada própria. A cobertura foi reconstruída em duas frentes:

•	Centroides reais de bairro preservados quando existentes.

•	Geocodificação por nome de bairro via Nominatim (OpenStreetMap), rodada localmente com cache resumível, controle de taxa e normalização de nomes (expansão de abreviações como JD→JARDIM, VL→VILA; remoção de acentos para casar bairros sem coordenada com gêmeos geolocalizados).

Resultado da cobertura:
Métrica	Valor

Bairros distintos geolocalizados	24.011 em 645 municípios

Ocorrências com bairro geolocalizado (pct_geo)	92,2%

Ocorrências exibidas no mapa (pct_mapa)	100%

A base do mapa tem duas listas de pontos: bairros (24.011 pontos geolocalizados, ~249.187 casos de VD ≈ 92,2%) e cidades_ng (623 pontos no centro do município, para bairros não geocodificados, ~20.993 casos ≈ 7,8%, marcados como posição aproximada na nota).

6. O que representa a "zona rural"
Cerca de 2,3% dos registros de violência doméstica (6.210) e 2,6% dos de feminicídio (37) têm o campo de bairro preenchido apenas como genérico — "RURAL", "ÁREA RURAL" ou "ZONA RURAL". Não há bairro específico: o endereço foi registrado apenas como a zona rural do município, e o histórico (que poderia conter o logradouro) é suprimido pela SSP por força do art. 31 da LAI.

No conjunto geolocalizado, esses casos haviam se empilhado em 242 pontos únicos, criando hotspots artificiais (como por exemplo em Franca 1.176, Carapicuíba 901, S. J. do Rio Preto 862) que apareciam entre os bairros mais violentos — o que era enganoso.

Para contornar essa falha, foi feito um tratamento aplicado com dot density, onde cada ponto rural foi distribuído pela zona rural do respectivo município (polígono do IBGE embutido no mapa, casado por geometria, não por nome). 

Os 242 pontos viraram 2.664 pontos dispersos pelas áreas periféricas da cidade, em zonas rurais, e o maior aglomerado num único ponto caiu de 1.176 → 15 casos. Esses casos foram retirados do ranking de bairros (Itaquera assumiu o 4º lugar) e a nota do mapa explica a aproximação. Os totais foram preservados exatamente (5.625 VD / 9 fe / 22 te apenas redistribuídos). 

Vale ressaltar que a localização para casos em áreas rurais são uma aproximação honesta de dado de área — não localização exata.

8. Perfil das vítimas e das ocorrências (infográfico)
Com base na mesma planilha, o código explorou um infográfico que foi embutido ao mapa, trazendo o perfil das vítimas das ocorrências fundamentadas nos levantamentos acima, variando por:
Faixa etária — vítimas de feminicídio/tentativa, Base 1, n = 1.406 com idade válida:

 Faixa	Casos
 
Menor de 18	50

18–25	232

26–30	208

31–40	440

41–50	293

51–60	111

61+	72


Cor/raça — Base 1, n = 1.415: Branca 655 (46,3%) · Parda 600 (42,4%) · Preta 122 (8,6%) · Amarela 1 (0,1%) · Ignorada 37 (2,6%).

Local da ocorrência — Bases 1+2: Residência 151.599 · Via Pública 98.577 · Internet 8.408 · Comércio/Shopping 2.817 · Bar/Restaurante 1.689 · Saúde 1.361 · Área Rural 1.352 · Lazer 758 · Ensino 624.

Horário — violência doméstica, Base 2, n = 213.853 com hora válida: Madrugada (0–5h) 28.861 (13,5%) · Manhã (6–11h) 45.416 (21,2%) · Tarde (12–17h) 59.155 (27,7%) · Noite (18–23h) 80.421 (37,6%).

Violência via internet — Base 2: WhatsApp 3.903 (46,4%) · Pela Internet 2.156 (25,6%) · Apps de Mensagens 1.895 (22,5%) · Instagram 257 (3,1%) · Facebook 178 (2,1%) · Outros 18 (0,2%).

Evolução mensal: série de 16 meses (jan/2025 a abr/2026), com violência doméstica num eixo e feminicídio + tentativas no outro.



8. Métodos do código
Mapa: Leaflet 1.9.4 + Leaflet.heat 0.2.0, bibliotecas embutidas (sem CDN; funciona offline). Estética escura; filtro segmentado (Todas / VD / Feminicídio / Tentativa) com gradiente de calor próprio para cada; marcadores clicáveis com pop-up (tipo, bairro e número de casos — sem endereço); painel lateral com cartões resumo, ranking dos 15 bairros e busca offline; legenda inferior (régua de intensidade + tamanho do ponto = nº de casos); limites municipais do IBGE (645 municípios, GeoJSON embutido, fonte tbrugz/geodata-br) com rótulos de cidade por zoom e chip de "qual município".

Infográfico: Chart.js 4.4.1 embutido; design editorial claro; KPIs animados, rosca de faixa etária e de cor/raça, barras de local e de internet, linha de evolução mensal com dois eixos e botões de alternância, grade de período do dia + sparkline de 24h, e barras empilhadas de feminicídio por idade.

Integração: o infográfico é carregado dentro do mapa por um iframe isolado (srcdoc) — isolamento total de CSS/JS garante que o código nativo e os dados do mapa permaneçam intactos.

Autossuficiência e validação: cada peça é um HTML único, sem dependências externas em execução (apenas a imagem de fundo de mapa é online e opcional — os pontos e o calor renderizam offline). Toda alteração foi validada em navegador headless (Playwright/Chromium), conferindo totais, renderização dos gráficos e integridade dos dados.

9. Privacidade e limites metodológicos
•	Dados primários, não estatística oficial. São extrações do Registro Digital de Ocorrências (R.D.O.); a estatística criminal oficial de SP segue a Resolução SSP nº 160/01. O total de B.O. sob uma natureza não representa a estatística criminal do estado.

•	Abrangência histórica. O R.D.O. só alcançou todos os municípios a partir de 2010, e seus campos passam por aperfeiçoamento contínuo.
•	Registro × circunscrição. Cerca de 60% dos B.O. são lavrados fora do município do fato.

•	Deduplicação. Para contagem de ocorrências, duplicidades são eliminadas pela combinação NOME_DELEGACIA + ANO_BO + NUM_BO (cada linha é uma vítima/objeto).

•	Privacidade. Não há endereços individuais (apenas bairro); campos que identificam pessoas são protegidos pelo art. 31 da Lei de Acesso à Informação, e os históricos não são fornecidos.

•	Classificação do feminicídio. A Base 1 segue o detalhamento da SSP (feminicídio/tentado dentro de homicídio doloso); o campo de rubrica é heterogêneo (≈936 como "Feminicídio" e ≈476 como "Homicídio art. 121"), o que convém ter em conta ao citar as contagens.

A planilha tem ~270 mil linhas de violência doméstica (cada linha = uma vítima/ocorrência, com 47 colunas) mais 1.415 de feminicídio. Embutir isso cru num HTML seria inviável (dezenas de MB e travaria o navegador). Então a condensação é, essencialmente, um "group by": 

agrupar as linhas por (município, bairro) e contar quantas caem em cada categoria.

Na prática, o pipeline faz:

1. Leitura em fluxo. A planilha (~69 MB) é lida em modo read only, linha a linha (openpyxl, iter_rows), sem carregar tudo na memória. Cada linha é classificada na categoria certa pelo campo de status: violência doméstica (Base 2), feminicídio consumado ou tentativa (Base 1, pelo flag C/T).

2. Agregação por bairro. Para cada linha, soma se 1 num contador da chave (cidade, bairro). Ao fim, milhares de linhas de um mesmo bairro viram uma única entrada com contagens. Por exemplo, todas as ocorrências do Grajau colapsam em:
   
{"c":"S.PAULO","b":"GRAJAU","lat":-23.78,"lng":-46.70,"vd":1416,"fe":3,"te":4}

É aí que mora a compressão: ~270 mil linhas × 47 colunas → ~24 mil entradas com 7 campos cada.

4. Uma coordenada por bairro. Cada grupo recebe um par lat/lng — o centroide das ocorrências daquele bairro que já tinham coordenada, ou, quando não havia, a coordenada do nome do bairro vinda da geocodificação (Nominatim, com cache). Isso transforma cada agregado num ponto.

5. Separação em duas listas. Os grupos com bairro geolocalizado vão para bairros (24.011 pontos ≈ 92,2% dos casos). Os bairros que não geocodificaram são somados no centro do município e vão para cidades_ng (623 pontos ≈ 7,8%), cada um guardando quantos bairros agregou (nb).
 
6. Pré cálculo do que a tela precisa. O ranking dos 15 maiores (top) e os totais/percentuais/datas (meta) já são calculados no build e gravados prontos, para a página não ter que recomputar nada.
Tudo isso é serializado como JSON compacto e colado dentro do HTML (window.__DADOS__).

Por que isso funciona no mapa de calor: cada ponto carrega um peso = número de casos. O Leaflet.heat soma os pesos por região, então 24 mil pontos ponderados reproduzem a densidade de 270 mil ocorrências — com o arquivo ficando em ~3,3 MB e renderizando offline.
Dois detalhes do mesmo princípio:

•	Zona rural (dispersão): o espalhamento que fizemos atua sobre os agregados já prontos, não sobre as linhas cruas — pega as 242 entradas rurais e redistribui a contagem de cada uma em vários pontos dentro do polígono do município, mantendo as somas idênticas.

•	Infográfico: mesma lógica, agregações ainda menores. Cada gráfico é só um vetorzinho de totais (faixa etária = 7 números, local = 9, meses = 16×2, horário = 24, cor/raça = 5, etc.), apurados num contador único sobre as bases e gravados como um objeto D minúsculo.

Resumindo: a "condensação" é agregar por bairro + uma coordenada por bairro + contagens por categoria, preservando exatamente os totais (270.295 / 374 / 1.041) — o mapa nunca precisa dos registros individuais, só das contagens georreferenciadas. 

________________________________________
Documento técnico de apoio editorial. Jornalista: Iago Yoshimi A. Seo · © 2026 — Todos os direitos reservados.

