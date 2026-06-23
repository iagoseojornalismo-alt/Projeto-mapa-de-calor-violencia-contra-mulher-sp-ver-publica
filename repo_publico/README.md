# Violência contra a mulher no Estado de São Paulo — versão de utilidade pública

Mapa de calor interativo e infográfico editorial sobre violência doméstica, feminicídio e tentativa de feminicídio no Estado de São Paulo, com base em dados obtidos via Lei de Acesso à Informação (LAI) junto à Secretaria de Segurança Pública de SP (SSP-SP).

**Esta é a versão gratuita, de utilidade pública e uso não comercial** do projeto. Ver [`LICENCA.md`](LICENCA.md) para os termos completos.

**Jornalista:** Iago Yoshimi A. Seo · **Período dos dados:** janeiro de 2025 a abril de 2026 (por data de registro/comunicação — ver metodologia).

\---

## ⚠️ Sobre esta versão

||Esta versão (utilidade pública)|Versão comercial (futura, para veículos)|
|-|-|-|
|**Uso**|Livre, não comercial|Licenciado para imprensa/comercial|
|**Mapa-base (tiles)**|CARTO (gratuito, **só para uso não comercial**)|Stadia Maps (plano pago, uso comercial liberado)|
|**Distribuição**|URL pública independente, este repositório|Oferecida diretamente aos veículos interessados|

As duas versões usam os **mesmos dados, mesma geolocalização, mesmo design** — a única diferença técnica é o provedor do mapa-base, escolhido conforme a licença de uso de cada versão.

\---

## O que tem aqui

* **`docs/index.html`** — mapa de calor (Leaflet) com 270.295 ocorrências de violência doméstica, 374 feminicídios e 1.041 tentativas, segmentável por categoria, com ranking de bairros, busca e infográfico embutido (aba lateral). Nota do mapa inclui as regras de uso desta versão.
* **`docs/infografico.html`** — versão standalone do infográfico (Chart.js).
* **`docs/METODOLOGIA.md`** — fonte dos dados, observações da SSP, e decisões de tratamento.
* **`docs/DICIONARIO\_DADOS.md`** — dicionário de campos fornecido pela SSP.
* **`docs/AUDITORIA.md`** — registro da auditoria de conciliação de totais feita antes da publicação.
* **`LICENCA.md`** — termos de uso desta versão (não comercial).

Os arquivos `.html` são **autocontidos** (Leaflet, Chart.js e todos os dados embutidos) — funcionam offline, sem build.

\---

## Incorporar (apenas usos não comerciais)

```html
<div style="position:relative;width:100%;padding-top:75%;">
  <iframe
    src="https://iagoseojornalismo-alt.github.io/Projeto-mapa-de-calor-violencia-contra-mulher-sp-ver-publica/"
    style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;"
    loading="lazy"
    title="Violência contra a mulher no Estado de São Paulo — mapa de calor">
  </iframe>
</div>
```

Lembrete: esta incorporação só é permitida para usos **não comerciais** (ver `LICENCA.md`). Veículos de imprensa interessados devem aguardar/solicitar a versão comercial.

\---

## Dados e metodologia (resumo)

* **Fonte:** SSP-SP, via LAI, sistemas SPVida (feminicídio/tentativa) e SPJ (violência doméstica).
* **Não são dados estatísticos oficiais** — são registros primários de boletins de ocorrência (R.D.O.).
* A base de violência doméstica é organizada por **data de registro**, não data do fato.
* 99,998% das ocorrências aparecem geolocalizadas no mapa.

Detalhamento completo em [`docs/METODOLOGIA.md`](docs/METODOLOGIA.md) e auditoria em [`docs/AUDITORIA.md`](docs/AUDITORIA.md).

\---

## Crédito e licença

Jornalista: **Iago Yoshimi A. Seo** · © 2026 · Dados: SSP-SP, via Lei de Acesso à Informação.

Ver [`LICENCA.md`](LICENCA.md) — uso livre para utilidade pública, **vedado uso comercial**.

