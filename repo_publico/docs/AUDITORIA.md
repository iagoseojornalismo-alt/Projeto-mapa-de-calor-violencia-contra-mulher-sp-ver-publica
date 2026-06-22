# Auditoria de dados — conciliação de totais

Antes da publicação, foi feita uma auditoria comparando os totais declarados no mapa contra a soma efetiva dos pontos desenhados (calor + marcadores clicáveis), e contra a planilha original da SSP-SP. Este documento registra o que foi encontrado e corrigido.

## O que foi conferido

1. Totais declarados no painel (violência doméstica, feminicídio, tentativa) batem com a contagem bruta da planilha (270.295 / 374 / 1.041) — **OK, sem alteração**.
2. Soma dos pontos efetivamente desenhados no mapa (camada de bairros geocodificados + camada de fallback por município) comparada ao total declarado.

## O que foi encontrado

A soma dos pontos do mapa estava **115 ocorrências de violência doméstica e 1 feminicídio abaixo** do total declarado — ou seja, esses casos não apareciam fisicamente em nenhum lugar do calor/mapa, embora contabilizados no painel.

Rastreamento, registro a registro:

| Causa | Casos | Município(s) | Correção |
|---|---|---|---|
| Nome de município com acento/apóstrofo não reconhecido no mecanismo de fallback (posição no centro do município) | 109 (VD) | Emilianópolis, Marabá Paulista, Luciânópolis, Gavião Peixoto, Santópolis do Aguapeí, Dirce Reis, Cruzália, Fernão, Turmalina, Aspásia, Nova Castilho, Campina do Monte Alegre, Santa Rita d'Oeste, São João do Pau d'Alho | Adicionados ao mesmo mecanismo de fallback já usado para outras 623 cidades, usando o centro do município (polígono IBGE já presente no mapa) |
| Grafia divergente do nome da cidade em uma única linha da planilha ("Araçatuba" com cedilha, vs. "Aracatuba" nas demais 1.414 linhas) | 1 (feminicídio) | Araçatuba | Mesclado à entrada já existente de Araçatuba |
| Cidade de registro fora do Estado de São Paulo (sem território no mapa estadual onde posicionar) | 6 (VD) | "Outro país", Brasília (DF), Niterói (RJ), Sacramento (MG), Planura (MG) | Não corrigível sem inventar localização — documentado como exceção irredutível na nota do mapa e no `pct_mapa` |

## Como foi corrigido

- As 109 ocorrências e o feminicídio foram adicionados usando **exatamente o mesmo mecanismo já existente no mapa** para cidades sem geocodificação por bairro (ponto no centro do município, com indicação de quantos boletins foram agrupados ali). Nenhum elemento visual novo foi criado; nenhum ponto já existente foi movido ou alterado.
- O percentual de cobertura do mapa (`pct_mapa`) foi recalculado com precisão real: **99,998%** (antes, um valor desatualizado de "100%" que — após o achado dos 6 casos fora do Estado — passaria a contradizer a própria nota do mapa).
- A nota do mapa foi atualizada para divulgar, de forma direta, a existência desses 6 casos fora do Estado e por que não aparecem no mapa.

## Conferência final (após correção)

```
soma interna (bairros + fallback por município):  vd = 270.289   fe = 374   te = 1.041
total declarado:                                  vd = 270.295   fe = 374   te = 1.041
diferença restante:                               vd =      6 (documentada, fora do Estado)   fe = 0   te = 0
```

A redistribuição de "área rural" (ver `METODOLOGIA.md`, item 3) foi reaplicada sobre a base já corrigida, preservando exatamente os totais por categoria (vd 5.625 / fe 9 / te 22 nos 242 registros redistribuídos).
