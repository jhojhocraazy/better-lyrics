<!--
  Seguranca: chaves de API (provedores de letras, TMDB/OMDb, servicos de video)
  NUNCA devem ser hardcoded neste projeto. Elas sao injetadas exclusivamente pelo
  usuario via localStorage, pelas configuracoes da interface visual. Nao adicione
  chaves reais a arquivos versionados.
-->

# AGENTS.md — Diretriz local de localização: better-lyrics

> **Herança obrigatória.** Toolchain, gates de CI, política de PR e convenções de código estão em
> [`AGENTS.upstream.md`](./AGENTS.upstream.md). Leia-o antes de qualquer mudança que não seja texto.
> Este arquivo governa **apenas** decisões semânticas de idioma; em caso de conflito sobre build, o
> upstream vence.

## 1. Domínio

Extensão de navegador (Chromium e Firefox) que lê o estado do player do YouTube Music e injeta letras
em tempo real sobre a interface, com página de opções, popup e escolha de fontes de letras.

O usuário é alguém ouvindo música enquanto trabalha: ele não "configura um plugin", ele quer a linha
certa destacada no segundo certo. Texto de UI aqui compete com a música por atenção — frases longas
são perdidas.

## 2. Onde o texto vive (verificado no clone)

| Caminho | Papel | Tratamento |
| --- | --- | --- |
| `_locales/en/messages.json` | fonte semântica de verdade | referência primária |
| `_locales/pt_BR/messages.json` | 643 chaves, ~115 KB, já publicado | baseline **auditável**, não dogma |
| `_locales/<outros>/messages.json` | demais idiomas | fora de escopo |
| `src/core/generated/locales.ts` | gerado a partir de `_locales/` | nunca editar à mão |
| `manifest.json` | `name` / `description` da extensão | limite de 132 caracteres na Chrome Web Store |
| `public/css/themes/` | temas, sem texto | fora de escopo |

## 3. Protocolo de inferência semântica

Nenhum termo é decidido por dicionário. A sequência é obrigatória:

1. **Localizar o consumo.** `grep` pela chave em `src/` para ver o componente, o espaço disponível e
   o que está ao redor. String sem contexto de renderização não é traduzível com segurança.
2. **Classificar o campo.** Rótulo de ação, estado do player, mensagem de erro, metadado de loja ou
   nome de formato técnico. Cada classe tem registro próprio: ação no infinitivo, estado descritivo,
   erro acionável.
3. **Inferir o eixo semântico.** Muitas chaves são posições num eixo, não palavras. Antes de verter um
   estado, identifique o eixo pelos irmãos no JSON e pelo componente consumidor (tempo? versão?
   disponibilidade? etapa do fluxo?). Traduzir a palavra isolada é o erro mais caro do projeto.
4. **Buscar evidência externa.** Como o próprio YouTube Music em pt-BR nomeia o mesmo conceito na
   tela correspondente? Como players concorrentes (Spotify, Deezer) nomeiam? Cite a fonte no
   relatório — "soa melhor" não é evidência.
5. **Testar naturalidade.** Leia como um brasileiro leria de passagem, não como revisor. Se a frase
   só faz sentido porque o inglês está por trás, reescreva.
6. **Registrar.** Toda decisão entra no handoff com alternativa rejeitada e motivo (seção 8).

## 4. Invariantes técnicas

- Chaves JSON, `$PLACEHOLDER$`, `{0}`, `%s`, URLs e nomes de arquivo permanecem byte a byte.
- Marcas e formatos não se traduzem: `YouTube Music`, `Spotify`, `Apple Music`, nomes de formato de
  letra e nomes de provedor.
- `messages.json` mantém a indentação de 2 espaços e a ordem das chaves.
- O conjunto de 643 chaves não muda de tamanho sem atualização do `en`.
- Nada de HTML ou markdown novo dentro de string que não tinha.

## 5. Critérios de aceitação

- Rótulo de opção ≤ 32 caracteres; descrição ≤ 120; descrição da store ≤ 132.
- Caixa de frase, sem ponto final em botão; zero gerúndio em ação.
- Consistência dentro do arquivo: o mesmo conceito tem sempre a mesma palavra.
- Zero decalque: nenhuma frase que só exista para espelhar a sintaxe inglesa.
- Acentuação completa; nenhum "nao", "voce" ou "musica".

## 6. Proibições

- Verter chave de estado ou termo técnico pela primeira acepção do dicionário, sem passar pelos passos
  2 e 3.
- Criar termo que nenhuma plataforma brasileira usa, ainda que seja "mais correto".
- Traduzir marca, nome de formato ou identificador de código.
- Editar `src/core/generated/locales.ts`.
- Tratar `_locales/pt_BR` como intocável ou como verdade: ele é baseline a auditar, e qualquer
  alteração nele exige justificativa registrada.

## 7. Verificação

```bash
npm run generate:locales    # após qualquer mudança em _locales/
npm run typecheck
npm run check:i18n-brand    # falha se termo protegido for traduzido
npm run lint
```

Valide o JSON com parser nativo antes de considerar pronto; vírgula sobrando derruba a extensão
inteira em runtime, não só a string.

## 8. Handoff

Entregue uma linha por decisão:

| chave | EN | pt-BR escolhido | evidência (arquivo:linha ou plataforma) | alternativa rejeitada | motivo |
| --- | --- | --- | --- | --- | --- |

Sem a coluna de evidência preenchida, a decisão é considerada não fundamentada.
