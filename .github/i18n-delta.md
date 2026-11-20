# Delta upstream — better-lyrics

- Gerado em: 2026-11-20T15:04:49.4180477+00:00
- Base local: cfe9b06ee4e068bc2c4b931463edd94edc9c0090
- Upstream: upstream/master / 631fb006a4f42699950ac34e92eacbe8abb5b20c
- Chaves pendentes: 4

## Chaves detectadas

```json
{
  "tool": "sync-check.ps1",
  "version": "1.0.0",
  "generatedAt": "2026-11-20T15:04:48.7253275+00:00",
  "root": "D:\\a\\better-lyrics",
  "mode": "nofetch",
  "summary": {
    "analyzed": 1,
    "updated": 0,
    "newStrings": 1,
    "removals": 0,
    "gaps": 0,
    "errors": 0,
    "pendingKeys": 4,
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
      "upstreamCommit": "631fb006a4f42699950ac34e92eacbe8abb5b20c",
      "baseCommit": "cfe9b06ee4e068bc2c4b931463edd94edc9c0090",
      "baseSource": "baseline",
      "ahead": 33,
      "behind": 13,
      "status": "Novas strings",
      "added": 4,
      "modified": 0,
      "removed": 0,
      "pending": 4,
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
          "upstreamKeys": 646,
          "added": [
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

| chave | EN | sugestão pt-BR | justificativa |
| --- | --- | --- | --- |
| `unison_credit_title` | Unison | Unison | Nome de provedor/fonte de letras — marca protegida (§4), não se traduz. |
| `unison_credit_one` | 1 contributor | 1 colaborador | Rótulo de contagem (eixo: número de pessoas). "Colaborador" é o termo usado por plataformas de créditos musicais em pt-BR; "contribuinte" é decalque fiscal. |
| `unison_credit_two` | 2 contributors | 2 colaboradores | Mesma classe e eixo de `unison_credit_one`; consistência de conceito exige a mesma palavra (§5). |
| `unison_credit_many` | $COUNT$ contributors | $COUNT$ colaboradores | Placeholder `$COUNT$` preservado byte a byte (§4); plural fixo como no EN, sem flexão condicional. |

Observações de handoff:
- As quatro chaves são novas (delta `added`), sem equivalente em `_locales/pt_BR` — não há baseline a auditar, apenas inserção na ordem do `en`.
- Evidência externa pendente de confirmação no componente consumidor: recomendo `grep -r "unison_credit_" src/` antes do merge para validar espaço de renderização (rótulo ≤ 32 caracteres, atendido) e se `$COUNT$` aparece em contexto de plural dinâmico.
- Nenhuma decisão aqui altera chaves existentes; `src/core/generated/locales.ts` não deve ser editado à mão (§6).

> Revise as sugestões e aplique apenas as chaves listadas, seguindo o AGENTS.md local. Este PR não altera os catálogos automaticamente.
