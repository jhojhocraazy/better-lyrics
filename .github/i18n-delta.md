# Delta upstream — better-lyrics

- Gerado em: 2026-11-27T16:22:34.9711976+00:00
- Base local: cfe9b06ee4e068bc2c4b931463edd94edc9c0090
- Upstream: upstream/master / 37efcdd864cd434d648e0e9bee6b90365d59a429
- Chaves pendentes: 8

## Chaves detectadas

```json
{
  "tool": "sync-check.ps1",
  "version": "1.0.0",
  "generatedAt": "2026-11-27T16:22:34.3047952+00:00",
  "root": "D:\\a\\better-lyrics",
  "mode": "nofetch",
  "summary": {
    "analyzed": 1,
    "updated": 0,
    "newStrings": 1,
    "removals": 0,
    "gaps": 0,
    "errors": 0,
    "pendingKeys": 8,
    "missingKeys": 0
  },
  "baselineUpdated": [],
  "repos": [
    {
      "name": "better-lyrics",
      "branch": "master",
      "head": "a3303bb870d136ef78a8eb714d19935bd720396f",
      "headShort": "a3303bb8",
      "upstreamRef": "upstream/master",
      "upstreamCommit": "37efcdd864cd434d648e0e9bee6b90365d59a429",
      "baseCommit": "cfe9b06ee4e068bc2c4b931463edd94edc9c0090",
      "baseSource": "baseline",
      "ahead": 33,
      "behind": 35,
      "status": "Novas strings",
      "added": 8,
      "modified": 0,
      "removed": 0,
      "pending": 8,
      "baseKeys": 642,
      "missingKeys": 0,
      "extraKeys": 0,
      "coveragePercent": 100.0,
      "dirtyFiles": [],
      "sourceDirty": [],
      "fetchError": "",
      "error": "",
      "warnings": [
        "Modo offline (-NoFetch): git fetch não executado."
      ],
      "files": [
        {
          "path": "_locales/en/messages.json",
          "target": "_locales/pt_BR/messages.json",
          "targetExists": true,
          "baseKeys": 642,
          "upstreamKeys": 650,
          "added": [
            "lyrics_rendererUnavailable",
            "lyrics_rendererUnavailableHintChromium",
            "lyrics_rendererUnavailableHintEdge",
            "lyrics_rendererUnavailableHintFirefox",
            "unison_credit_many",
            "unison_credit_one",
            "unison_credit_title",
            "unison_credit_two"
          ],
          "modified": [],
          "removed": [],
          "missing": [],
          "extra": [],
          "warning": ""
        }
      ]
    }
  ]
}

```

## Sugestões DeepSeek

Preciso do conteúdo das 8 chaves em `_locales/en/messages.json` (mensagem + description, quando houver) para traduzir com contexto. O delta lista apenas as chaves, não os valores. Sem o EN não consigo preencher a coluna "EN" nem justificar com evidência.

Peço que cole o trecho do `en/messages.json` com:

- `lyrics_rendererUnavailable`
- `lyrics_rendererUnavailableHintChromium`
- `lyrics_rendererUnavailableHintEdge`
- `lyrics_rendererUnavailableHintFirefox`
- `unison_credit_many`
- `unison_credit_one`
- `unison_credit_title`
- `unison_credit_two`

Além disso, para cumprir o passo 1 do protocolo (localizar o consumo), seria útil o resultado de:

```bash
grep -rn "lyrics_rendererUnavailable\|unison_credit_" src/
```

Com isso entrego a tabela no formato da seção 8 (chave | EN | pt-BR | evidência | alternativa rejeitada | motivo), respeitando limites (rótulo ≤ 32, descrição ≤ 120), sem gerúndio em ação e com acentuação completa.

> Revise as sugestões e aplique apenas as chaves listadas, seguindo o AGENTS.md local. Este PR não altera os catálogos automaticamente.
