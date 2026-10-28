# DeckCraft — working notes for Claude

## Politica de validacao local

Siga a politica obrigatoria de [validacao documental e confirmacao para testes](AGENTS.md#validacao-documental-e-confirmacao-para-testes). Commits exclusivamente documentais elegiveis usam revisao do diff, `git diff --check`, conferencia de links locais e coerencia das instrucoes; informe a dispensa da validacao completa. Testes, compilacao, lint de codigo e CI exigem explicacao previa de necessidade e alcance e confirmacao explicita do usuario antes de executar. Comandos e rotinas abaixo estao sujeitos a essa politica, inclusive verificacoes iniciais; autonomia nao dispensa essa confirmacao.

Read [AGENTS.md](AGENTS.md) first: its rules (asset policy, clean room, never crash) bind you and
win over anything here.

## Start every session
1. Read `plan/STATUS.md`, then the current milestone in `plan/execution-plan.md`.
2. Read `../../craftrules/AGENTS.md` and the standards it lists for your task.
3. For changes requiring code validation, propose a baseline `cargo xtask ci` run and await explicit user confirmation under AGENTS.md. Skip it for exclusively documentary changes.

## Habits
- Every user-visible action is a command with tests (`crates/engine/src/cmd/*`).
- Look at UI changes: `deckcraft --sample --control 7990` + `ui.screenshot`, or
  `deckcraft-cli render`.
- Commit after each landed arc (`M<n>.<k>: what`) and push to `origin main`.
- Keep `ROADMAP.md`, the progress docs in `docs/` (AGENTS.md §7) and `plan/STATUS.md` current.
- Ask for explicit user confirmation before tests or code validation as required by AGENTS.md; record other owner decisions in `plan/STATUS.md`.
