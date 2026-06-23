# Guia Completo dos Comandos do Claude Code

> Referência em português de **todos os comandos** do Claude Code: comandos de barra (`/`),
> comandos de terminal (`claude ...`), atalhos de teclado e modos especiais.
> Baseado na documentação oficial (versão 2.1.x). Atualizado em 23/06/2026.

**Como usar este guia:** dentro do Claude Code você digita `/` para ver a lista de comandos disponíveis.
No terminal (PowerShell/CMD) você digita `claude ...`. Nem todo comando aparece para todo mundo —
alguns dependem do seu plano, sistema operacional ou ambiente.

---

## Índice
1. [Comandos de barra (`/`) — dentro do Claude Code](#1-comandos-de-barra--dentro-do-claude-code)
2. [Comandos de terminal (CLI) — no PowerShell](#2-comandos-de-terminal-cli--no-powershell)
3. [Flags (opções) da linha de comando](#3-flags-opções-da-linha-de-comando)
4. [Atalhos de teclado](#4-atalhos-de-teclado)
5. [Modos especiais e prefixos](#5-modos-especiais-e-prefixos)
6. [Modo Vim (edição estilo Vim)](#6-modo-vim-edição-estilo-vim)
7. ["O que isso significa pra mim" — guia rápido do dia a dia](#7-o-que-isso-significa-pra-mim--guia-rápido-do-dia-a-dia)

---

## 1. Comandos de barra (`/`) — dentro do Claude Code

Digitados no início da mensagem, dentro de uma sessão do Claude Code. O texto após o comando vira "argumento".
`<arg>` = obrigatório, `[arg]` = opcional.

### Configuração e início de projeto

| Comando | O que faz (em português) |
|---|---|
| `/init` | Cria um arquivo `CLAUDE.md` inicial documentando o seu projeto (guia para o Claude). |
| `/memory` | Edita os arquivos de memória `CLAUDE.md`; liga/desliga a memória automática e mostra suas entradas. |
| `/config [chave=valor]` | Abre as configurações (tema, modelo, estilo de saída...). Pode setar direto, ex.: `/config theme=dark`. Apelido: `/settings`. |
| `/permissions` | Gerencia regras de permissão (permitir / perguntar / negar) das ferramentas. Apelido: `/allowed-tools`. |
| `/agents` | Cria e gerencia subagentes de IA (delegação de tarefas). |
| `/mcp` | Gerencia conexões com servidores MCP e autenticação OAuth. |
| `/hooks` | Vê e configura os *hooks* (ganchos) que disparam em eventos de ferramentas. |
| `/skills` | Lista as *skills* (habilidades) disponíveis; permite ocultar alguma. |
| `/plugin [subcomando]` | Gerencia plugins (`list`, `install`, `enable`, `disable`...). |
| `/reload-plugins [--force]` | Recarrega plugins sem reiniciar. |
| `/reload-skills` | Re-escaneia skills/comandos adicionados durante a sessão. |
| `/statusline` | Configura a barra de status do Claude Code. |
| `/keybindings` | Abre o arquivo de atalhos de teclado para personalizar. |
| `/theme` | Muda o tema de cores (claro, escuro, automático, daltônico...). |
| `/terminal-setup` | Configura o atalho **Shift+Enter** (nova linha) no seu terminal (VS Code, Cursor etc.). |
| `/ide` | Gerencia a integração com a IDE e mostra o status. |

### Durante a tarefa

| Comando | O que faz (em português) |
|---|---|
| `/plan [descrição]` | Entra no **modo de planejamento** (planeja antes de executar). Ex.: `/plan corrigir o bug de login`. |
| `/model [modelo]` | Troca o modelo de IA (Opus, Sonnet, Haiku, Fable) e salva como padrão. |
| `/effort [nível]` | Ajusta o "esforço" de raciocínio: `low`, `medium`, `high`, `xhigh`, `max`, `ultracode`. |
| `/fast [on\|off]` | Liga/desliga o **modo rápido** (mesmo Opus, com saída mais veloz). |
| `/context [all]` | Mostra o uso do contexto (janela) num grid colorido, com dicas de otimização. |
| `/compact [instruções]` | Resume a conversa para liberar contexto. Pode focar o resumo em algo. |
| `/clear [nome]` | Começa uma conversa nova com contexto vazio (mantém a memória do projeto). Apelidos: `/reset`, `/new`. |
| `/btw <pergunta>` | Pergunta rápida "a propósito" sem poluir o histórico da conversa. |
| `/goal [condição]` | Define uma meta: o Claude continua trabalhando entre turnos até cumprir. |
| `/recap` | Gera um resumo de uma linha do que aconteceu na sessão. |
| `/copy [N]` | Copia a última resposta do Claude (ou a N-ésima) para a área de transferência. |
| `/export [arquivo]` | Exporta a conversa como texto (arquivo ou área de transferência). |
| `/diff` | Abre um visualizador interativo das mudanças não commitadas e por turno. |
| `/focus` | Mostra só o essencial (seu último prompt + resumo das ações + resposta final). |
| `/insights` | Gera um relatório analisando suas sessões (padrões, pontos de atrito). |

> **Nota: `/plan` × `Shift+Tab` × `/ultraplan` — as três formas de planejar**
> Todas levam ao **modo de planejamento** (o Claude propõe um plano e só executa após sua aprovação).
> A diferença é só *como* você entra nele:
> - **`/plan [descrição]`** — comando que entra no modo já com a tarefa. Ex.: `/plan corrigir o bug de login`.
> - **`Shift+Tab`** — atalho de teclado que alterna para o modo de planejamento (sem digitar).
> - **`/ultraplan <prompt>`** — o "primo grande": rascunha o plano numa sessão **na nuvem**, você revisa no navegador e manda executar. Para tarefas maiores.

### Trabalho em paralelo e em segundo plano

| Comando | O que faz (em português) |
|---|---|
| `/background [prompt]` | Destaca a sessão para rodar como **agente em segundo plano**, liberando o terminal. Apelido: `/bg`. |
| `/tasks` | Vê e gerencia tudo que está rodando em segundo plano. Também como `/bashes`. |
| `/fork <diretriz>` | Cria um subagente que herda a conversa e trabalha numa tarefa enquanto você continua. |
| `/branch [nome]` | Ramifica a conversa neste ponto para tentar outra direção sem perder a original. |
| `/batch <instrução>` | (Skill) Decompõe uma mudança grande em 5–30 unidades e roda cada uma em paralelo (worktrees). |
| `/loop [intervalo] [prompt]` | (Skill) Roda um prompt repetidamente. Ex.: `/loop 5m verifique se o deploy terminou`. Apelido: `/proactive`. |
| `/workflows` | Abre a visão de progresso dos *workflows* (orquestração de vários subagentes). |
| `/stop` | Para a sessão em segundo plano à qual você está conectado. |

### Antes de "entregar" (revisão de código)

| Comando | O que faz (em português) |
|---|---|
| `/code-review [nível] [--fix] [--comment] [alvo]` | (Skill) Revisa o *diff* atual buscando bugs e melhorias. `--fix` aplica correções; `ultra` roda revisão profunda na nuvem. |
| `/review [PR]` | Revisa um Pull Request do GitHub (mesma engine do `/code-review`, só leitura). |
| `/simplify [alvo]` | (Skill) Revisa o código só para limpeza/simplificação e aplica os ajustes (não caça bugs). |
| `/security-review` | Analisa as mudanças pendentes em busca de vulnerabilidades de segurança. |
| `/ultrareview [PR]` | Revisão profunda multiagente na nuvem. Prefira `/code-review ultra` (este é apelido). |
| `/ultraplan <prompt>` | Rascunha um plano numa sessão na nuvem, revisa no navegador e executa. |
| `/verify` | (Skill) Confirma que a mudança funciona rodando o app de verdade (não só testes). |
| `/run` | (Skill) Inicia e dirige o app do projeto para ver a mudança funcionando. |
| `/run-skill-generator` | (Skill) Ensina o `/run` e o `/verify` a iniciar o app do seu projeto. |
| `/autofix-pr [prompt]` | Cria sessão na nuvem que vigia o PR da branch e empurra correções quando o CI falha. |
| `/install-github-app` | Configura o app do Claude (GitHub Actions) no repositório. |

### Entre sessões / continuidade

| Comando | O que faz (em português) |
|---|---|
| `/resume [sessão]` | Retoma uma conversa por ID/nome, ou abre o seletor de sessões. Apelido: `/continue`. |
| `/rename [nome]` | Renomeia a sessão atual (mostra o nome na barra). |
| `/rewind` | Volta a conversa e/ou o código a um ponto anterior (checkpoints). Apelidos: `/checkpoint`, `/undo`. |
| `/cd <caminho>` | Move a sessão para um novo diretório de trabalho (preserva o cache). |
| `/add-dir <caminho>` | Adiciona um diretório de trabalho para acesso a arquivos na sessão atual. |
| `/teleport` | Puxa uma sessão do "Claude Code na web" para este terminal. Apelido: `/tp`. |
| `/remote-control` | Permite controlar esta sessão local a partir do claude.ai. Apelido: `/rc`. |
| `/desktop` | Continua a sessão no app Claude Code Desktop. Apelido: `/app`. |
| `/remote-env` | Escolhe o ambiente padrão para agentes na nuvem. |

### Conta, ajuda e diagnóstico

| Comando | O que faz (em português) |
|---|---|
| `/help` | Mostra a ajuda e a lista de comandos disponíveis. |
| `/login` | Entra na sua conta Anthropic. |
| `/logout` | Sai da sua conta Anthropic. |
| `/status` | Abre o painel de status (versão, modelo, conta, conectividade). |
| `/usage` | Mostra custo da sessão, limites do plano e estatísticas. Apelidos: `/cost`, `/stats`. |
| `/usage-credits` | Configura créditos de uso para continuar quando bater o limite. |
| `/doctor` | Diagnostica a saúde da instalação e das configurações (tecle `f` para o Claude corrigir). |
| `/debug [descrição]` | (Skill) Liga o log de depuração e investiga problemas da sessão. |
| `/feedback [relato]` | Envia feedback / reporta bug com o contexto da sessão. Apelidos: `/bug`, `/share`. |
| `/release-notes` | Vê o changelog (novidades) por versão. |
| `/privacy-settings` | Vê e ajusta configurações de privacidade (planos Pro/Max). |
| `/upgrade` | Abre a página para mudar para um plano superior. |
| `/heapdump` | Salva um snapshot de memória no `~/Desktop` para diagnosticar uso alto de memória. |

### Skills e workflows agendados

| Comando | O que faz (em português) |
|---|---|
| `/deep-research <pergunta>` | (Workflow) Faz buscas na web, cruza fontes e gera um relatório com citações. |
| `/claude-api [migrate\|...]` | (Skill) Carrega referência da Claude API para a linguagem do seu projeto. |
| `/fewer-permission-prompts` | (Skill) Cria uma allowlist no `settings.json` para reduzir pedidos de permissão. |
| `/schedule [descrição]` | Cria/edita/lista *routines* (tarefas) que rodam na nuvem em horário agendado. Apelido: `/routines`. |
| `/team-onboarding` | Gera um guia de integração para a equipe a partir do seu histórico de uso. |
| `/web-setup` | Conecta sua conta GitHub ao "Claude Code na web" usando o `gh` local. |

### Extras / interface

| Comando | O que faz (em português) |
|---|---|
| `/tui [default\|fullscreen]` | Define o renderizador da interface (modo tela cheia sem flicker). |
| `/color [cor]` | Muda a cor da barra de prompt da sessão. |
| `/voice [hold\|tap\|off]` | Liga/desliga a ditação por voz (requer conta claude.ai). |
| `/scroll-speed` | Ajusta a velocidade de rolagem do mouse (modo tela cheia). |
| `/sandbox` | Liga/desliga o modo *sandbox* (isolamento). |
| `/advisor [modelo\|off]` | Liga/desliga a ferramenta "conselheira" (consulta um 2º modelo em momentos-chave). |
| `/chrome` | Configura a integração "Claude no Chrome". |
| `/powerup` | Lições interativas rápidas para descobrir recursos do Claude Code. |
| `/radio` | Abre a rádio lo-fi "Claude FM" no navegador. |
| `/mobile` | Mostra QR code para baixar o app móvel. Apelidos: `/ios`, `/android`. |
| `/passes` | Compartilha uma semana grátis de Claude Code com amigos (se elegível). |
| `/stickers` | Pede adesivos do Claude Code. |
| `/exit` | Sai do Claude Code. Apelido: `/quit`. |

> **Observação:** servidores MCP podem expor *prompts* que aparecem como comandos no formato
> `/mcp__<servidor>__<prompt>`. O comando `/vim` foi **removido** na v2.1.92 — agora use `/config` → Editor mode.
> O `/pr-comments` foi removido na v2.1.91 (peça direto ao Claude para ver os comentários do PR).

---

## 2. Comandos de terminal (CLI) — no PowerShell

Digitados no terminal (não dentro do Claude Code).

| Comando | O que faz (em português) |
|---|---|
| `claude` | Inicia uma sessão interativa. |
| `claude "pergunta"` | Inicia a sessão já com um prompt inicial. |
| `claude -p "pergunta"` | Modo "print": responde e sai (ideal para scripts). |
| `cat arquivo \| claude -p "..."` | Processa conteúdo vindo de um *pipe*. |
| `claude -c` | Continua a conversa mais recente do diretório atual. |
| `claude -c -p "..."` | Continua a conversa via modo print. |
| `claude -r "sessão" "..."` | Retoma uma sessão por ID ou nome. |
| `claude update` | Atualiza para a última versão. |
| `claude install [versão]` | Instala/reinstala o binário nativo (ex.: `stable`, `latest` ou `2.1.118`). |
| `claude auth login` | Entra na conta Anthropic (`--console` para faturar via API; `--sso` para SSO). |
| `claude auth logout` | Sai da conta Anthropic. |
| `claude auth status` | Mostra o status de autenticação (JSON; `--text` para legível). |
| `claude agents` | Abre a "agent view" para monitorar/disparar sessões em segundo plano. |
| `claude attach <id>` | Conecta-se a uma sessão em segundo plano neste terminal. |
| `claude logs <id>` | Mostra a saída recente de uma sessão em segundo plano. |
| `claude respawn <id>` | Reinicia uma sessão em segundo plano mantendo a conversa. |
| `claude stop <id>` | Para uma sessão em segundo plano (também `claude kill`). |
| `claude rm <id>` | Remove uma sessão em segundo plano da lista (transcrição fica salva). |
| `claude mcp` | Configura servidores MCP. |
| `claude mcp login <nome>` | Faz o fluxo OAuth de um servidor MCP pela linha de comando. |
| `claude mcp logout <nome>` | Limpa as credenciais OAuth de um servidor MCP. |
| `claude config` | Gerencia configurações pela linha de comando. |
| `claude plugin` | Gerencia plugins (apelido: `claude plugins`). |
| `claude project purge [caminho]` | Apaga o estado local do projeto (transcrições, logs, histórico...). |
| `claude remote-control` | Inicia um servidor de Controle Remoto (controlar via claude.ai/app). |
| `claude setup-token` | Gera um token OAuth de longa duração para CI e scripts. |
| `claude auto-mode defaults` | Imprime as regras do classificador do "auto mode" (JSON). |
| `claude daemon status` | Mostra o estado do supervisor de sessões em segundo plano. |
| `claude daemon stop --any` | Para o supervisor de sessões em segundo plano. |
| `claude ultrareview [alvo]` | Roda a ultrarrevisão de forma não-interativa (imprime os achados). |
| `claude --version` (`-v`) | Mostra o número da versão. |
| `claude --help` (`-h`) | Mostra a ajuda. |

> Se você digitar errado, o Claude Code sugere o mais próximo. Ex.: `claude udpate` → "Did you mean claude update?".

---

## 3. Flags (opções) da linha de comando

As mais úteis. (`claude --help` não lista todas — a ausência ali não significa indisponível.)

### Modelo e raciocínio
| Flag | O que faz |
|---|---|
| `--model <modelo>` | Define o modelo da sessão (`sonnet`, `opus`, `haiku`, `fable` ou ID completo). |
| `--fallback-model <lista>` | Modelo(s) reserva quando o principal está sobrecarregado/indisponível. |
| `--effort <nível>` | Nível de esforço: `low`, `medium`, `high`, `xhigh`, `max`. |
| `--advisor <modelo>` | Liga a ferramenta conselheira (`opus`, `sonnet`, `fable`...). |

### Modo "print" / automação (scripts)
| Flag | O que faz |
|---|---|
| `--print`, `-p` | Imprime a resposta sem modo interativo. |
| `--output-format <fmt>` | Formato de saída: `text`, `json`, `stream-json`. |
| `--input-format <fmt>` | Formato de entrada: `text`, `stream-json`. |
| `--json-schema '<schema>'` | Saída validada conforme um JSON Schema (modo print). |
| `--max-turns <n>` | Limita o número de turnos (modo print). |
| `--max-budget-usd <valor>` | Teto de gasto em dólares antes de parar (modo print). |
| `--bare` | Modo mínimo: pula descoberta de hooks/skills/plugins/MCP/CLAUDE.md (mais rápido). |
| `--verbose` | Log detalhado, turno a turno. |

### Permissões e ferramentas
| Flag | O que faz |
|---|---|
| `--permission-mode <modo>` | Inicia em um modo: `default`, `acceptEdits`, `plan`, `auto`, `dontAsk`, `bypassPermissions`. |
| `--dangerously-skip-permissions` | **⚠️ Pula todos os pedidos de permissão.** Use com muito cuidado. |
| `--allow-dangerously-skip-permissions` | Adiciona o `bypassPermissions` ao ciclo do Shift+Tab sem iniciar nele. |
| `--allowedTools "..."` | Ferramentas que executam sem pedir permissão. |
| `--disallowedTools "..."` | Regras de negação de ferramentas. |
| `--tools "Bash,Edit,Read"` | Restringe quais ferramentas embutidas o Claude pode usar. |

### Diretórios, sessão e contexto
| Flag | O que faz |
|---|---|
| `--add-dir <caminho>` | Adiciona diretórios de trabalho. |
| `--resume <id>`, `-r` | Retoma uma sessão específica (ou abre o seletor). |
| `--continue`, `-c` | Carrega a conversa mais recente do diretório. |
| `--fork-session` | Ao retomar, cria um novo ID em vez de reutilizar o original. |
| `--session-id <uuid>` | Usa um ID de sessão específico. |
| `--name <nome>`, `-n` | Define um nome de exibição para a sessão. |
| `--worktree <nome>`, `-w` | Inicia em um *git worktree* isolado. |
| `--ide` | Conecta automaticamente à IDE no início. |
| `--chrome` / `--no-chrome` | Liga/desliga a integração com o Chrome. |

### MCP, plugins e prompt do sistema
| Flag | O que faz |
|---|---|
| `--mcp-config <arquivo>` | Carrega servidores MCP de arquivos/strings JSON. |
| `--strict-mcp-config` | Usa só os servidores MCP do `--mcp-config`. |
| `--plugin-dir <caminho>` | Carrega um plugin de uma pasta/`.zip` só nesta sessão. |
| `--settings <arquivo>` | Caminho (ou JSON) de configurações que sobrescrevem o `settings.json`. |
| `--system-prompt "..."` | Substitui todo o prompt do sistema. |
| `--append-system-prompt "..."` | Acrescenta texto ao final do prompt do sistema padrão. |
| `--safe-mode` | Inicia com todas as customizações desativadas (para diagnosticar). |
| `--debug "api,mcp"` | Liga o modo de depuração com filtro de categorias. |

---

## 4. Atalhos de teclado

### Controles gerais
| Atalho | O que faz |
|---|---|
| `Esc` | Interrompe o Claude no meio do turno (mantém o trabalho feito). |
| `Esc` `Esc` | Com texto digitado: limpa e salva no histórico. Vazio: abre o menu de *rewind* (checkpoints). |
| `Ctrl+C` | Interrompe a operação; ou limpa a entrada; pressionado de novo (vazio) sai do Claude Code. |
| `Ctrl+D` | Sai da sessão do Claude Code (sinal EOF). |
| `Ctrl+L` | Redesenha a tela (recupera display embaralhado). |
| `Ctrl+O` | Liga/desliga o visualizador de transcrição (detalhes de ferramentas). |
| `Ctrl+R` | Busca reversa no histórico de comandos. |
| `Ctrl+B` | Joga a tarefa/comando atual para segundo plano (tmux: duas vezes). |
| `Ctrl+T` | Liga/desliga a lista de tarefas. |
| `Ctrl+G` ou `Ctrl+X Ctrl+E` | Abre o prompt no seu editor de texto padrão. |
| `Ctrl+V` / `Alt+V` (Windows/WSL) | Cola imagem da área de transferência (insere chip `[Image #N]`). |
| `Ctrl+X Ctrl+K` | Para todos os subagentes em segundo plano (duas vezes em 3s para confirmar). |
| `Shift+Tab` (ou `Alt+M`) | Alterna os modos de permissão (`default`, `acceptEdits`, `plan`, `auto`...). |
| `Alt+P` (Win/Linux) | Troca o modelo sem limpar o prompt. |
| `Alt+T` (Win/Linux) | Liga/desliga o *extended thinking* (raciocínio estendido). |
| `Alt+O` (Win/Linux) | Liga/desliga o **modo rápido**. |
| `↑` / `↓` (ou `Ctrl+P`/`Ctrl+N`) | Move o cursor; nas bordas, navega o histórico de comandos. |
| `←` / `→` | Navega entre abas de diálogos/menus. |

### Edição de texto
| Atalho | O que faz |
|---|---|
| `Ctrl+A` | Vai para o início da linha. |
| `Ctrl+E` | Vai para o fim da linha. |
| `Ctrl+K` | Apaga até o fim da linha (guarda para colar). |
| `Ctrl+U` | Apaga do cursor até o início da linha (guarda para colar). |
| `Ctrl+W` | Apaga a palavra anterior (no Windows, `Ctrl+Backspace` também). |
| `Ctrl+Y` | Cola o texto apagado com `Ctrl+K/U/W`. |
| `Alt+B` / `Alt+F` | Move o cursor uma palavra para trás / para frente. |

### Nova linha (entrada multilinha)
| Atalho | Contexto |
|---|---|
| `\` + `Enter` | Funciona em qualquer terminal. |
| `Ctrl+J` | Funciona em qualquer terminal, sem configurar. |
| `Shift+Enter` | Nativo em alguns terminais; nos demais (VS Code, Cursor...) rode `/terminal-setup`. |

---

## 5. Modos especiais e prefixos

| Prefixo / tecla | O que faz |
|---|---|
| `/` (no início) | Executa um comando ou skill. |
| `!` (no início) | **Modo shell:** roda um comando direto, adiciona a saída ao contexto e o Claude responde a ela. Ex.: `! npm test`, `! git status`. |
| `@` | **Menção de arquivo:** dispara o autocompletar de caminhos de arquivo para referenciar no prompt. |
| Colar imagem | `Ctrl+V`/`Alt+V` insere a imagem para você referenciar no texto. |

> O modo shell (`!`) sai com `Esc`, `Backspace` ou `Ctrl+U` no prompt vazio, e aceita autocompletar
> com `Tab` a partir de comandos `!` anteriores do projeto.

---

## 6. Modo Vim (edição estilo Vim)

Ative em `/config` → **Editor mode**. Principais comandos no modo NORMAL:

**Trocar de modo:** `Esc` (NORMAL), `i`/`I` (inserir antes/início), `a`/`A` (inserir depois/fim), `o`/`O` (abrir linha abaixo/acima), `v`/`V` (seleção visual).

**Navegar:** `h`/`j`/`k`/`l` (←↓↑→), `w` (próxima palavra), `e` (fim da palavra), `b` (palavra anterior), `0` (início da linha), `$` (fim da linha), `^` (1º caractere não-branco), `gg`/`G` (início/fim), `f{c}`/`F{c}` (pular para caractere).

**Editar:** `x` (apaga caractere), `dd` (apaga linha), `D` (apaga até o fim), `dw`/`cw`/`yw` (apagar/mudar/copiar palavra), `cc` (muda linha), `yy`/`Y` (copia linha), `p`/`P` (cola depois/antes), `u` (desfaz), `.` (repete a última mudança), `>>`/`<<` (indenta/desindenta).

**Objetos de texto** (com `d`, `c`, `y`): `iw`/`aw` (palavra), `i"`/`a"` (aspas), `i(`/`a(` (parênteses), `i{`/`a{` (chaves), etc.

---

## 7. "O que isso significa pra mim" — guia rápido do dia a dia

Tradução prática dos comandos que mais valem a pena no uso comum:

- **Conversa ficou enorme e lenta?**
  - `/compact` → resume e libera espaço **mantendo** a conversa.
  - `/clear` → começa **do zero** (mantém só a memória do projeto). Use ao trocar de assunto.
  - `/context` → mostra "onde está indo" a memória, se quiser entender o consumo.

- **Quer ver quanto está gastando?** `/usage` (ou `/cost`) mostra custo e limites do plano.

- **Fechou o Claude e quer voltar de onde parou?** `claude -c` (no terminal) ou `/resume` (dentro). Para nomear sessões e achar depois: `claude -n "meu-trabalho"`.

- **Errou e quer desfazer mudanças no código/conversa?** `/rewind` volta a um ponto anterior (checkpoint). É a sua "rede de segurança".

- **Quer planejar antes de o Claude mexer em tudo?** `/plan` (ou `Shift+Tab` até o modo *plan*). Ele propõe e só executa após sua aprovação.

- **Algo parou de funcionar?** `/doctor` diagnostica a instalação; `/status` mostra versão, modelo e conexão.

- **Quer rodar um comando do sistema rápido sem sair da conversa?** Use `!` na frente. Ex.: `! ipconfig`.

- **Quer apontar um arquivo específico para o Claude olhar?** Digite `@` e comece a escrever o caminho.

- **Trocar o nível de "capricho" da resposta:** `/model` (troca o modelo) e `/effort` (quão fundo ele pensa). `/fast` deixa o Opus mais ágil.

- **Acabar a tarefa:** `/exit` (ou `Ctrl+D`) para sair.

---

*Gerado pelo Claude Code (engenheiro de informática pessoal do Edney) a partir da documentação oficial em code.claude.com/docs. Para a referência sempre atualizada, use `/help` dentro do Claude Code ou `claude --help` no terminal.*
