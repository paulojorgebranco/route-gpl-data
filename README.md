# Route GPL — dados

Preços e localizações de postos de **GPL Auto** em Portugal, reconstruídos duas
vezes por dia a partir de fontes públicas e servidos como ficheiros estáticos.

Este repositório contém **apenas dados gerados**. O código que os constrói e a
app que os consome vivem noutro sítio.

## Como usar

O ponto de entrada é o manifesto, num endereço fixo:

```
https://paulojorgebranco.github.io/route-gpl-data/v1/pt/manifest.json
```

```json
{
  "schema_version": 1,
  "country": "PT",
  "generated_at": "2026-08-27T06:00:00+00:00",
  "station_count": 483,
  "station_count_with_price": 422,
  "data_url": "stations-e3c5f0f23a.json",
  "min_app_version": "1.0.0",
  "message": null,
  "license": "ODbL-1.0",
  "sources": [ { "id": "dgeg", "status": "ok", "station_count": 422 } ]
}
```

`data_url` é relativo ao manifesto e leva no nome o *hash* do conteúdo: se nada
mudou, o nome também não muda, e quem já tem esse ficheiro não precisa de o
voltar a descarregar.

O caminho tem o país (`v1/pt/`) para poder crescer sem partir quem já lê.

### Campos de um posto

| Campo | Notas |
|---|---|
| `name` | Nome para mostrar, limpo |
| `official_name` | O nome tal como o operador o declarou à DGEG |
| `lpg_price`, `petrol_price` | €/litro. `null` quando a fonte não os publica |
| `price_updated_at` | Quando o operador declarou o preço, hora de Portugal |
| `opening_hours`, `phone` | Vindos do OpenStreetMap, quando existem |
| `sources` | `dgeg`, `osm`, ou ambos |

### `history/`

Um retrato dos preços por dia, `YYYY-MM-DD.json`, desde o primeiro dia.

## De onde vêm os dados

| Fonte | O que dá |
|---|---|
| **DGEG** — Direção-Geral de Energia e Geologia | Preços declarados pelos operadores, actualizados diariamente |
| **OpenStreetMap** (via Overpass) | Localizações, horários, telefones, e postos que a DGEG não lista |

Dois registos a menos de 250 m são tratados como o mesmo posto físico: o preço
vem da DGEG, o horário e o telefone do OSM.

## Garantias, e o que não é garantido

Uma construção só é publicada se passar as validações: pelo menos 200 postos com
preço, preço mediano dentro da gama do GPL, e nenhuma quebra superior a 30 %
face à construção anterior. Quando falha, **a última versão boa fica no ar** — um
dia de dados velhos é preferível a um dia de dados errados.

Os preços são **declarados, não observados**: um operador pode ter declarado um
preço que entretanto mudou. `price_updated_at` diz sempre de quando é.

## Licença

Estes ficheiros fundem dados do OpenStreetMap, por isso são uma **base de dados
derivada** e são distribuídos sob a
[Open Database License (ODbL) v1.0](https://opendatacommons.org/licenses/odbl/1-0/).

Ao reutilizá-los, mantenha a atribuição:

> Preços: DGEG — Direção-Geral de Energia e Geologia.
> Localizações e horários: © contribuidores do OpenStreetMap, sob ODbL.

Este projecto não é afiliado, patrocinado nem aprovado pela DGEG nem pela
OpenStreetMap Foundation.
