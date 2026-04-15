# Contribuindo para Harness Copilot Skill

Obrigado pelo interesse em contribuir para a **Harness Copilot Skill**! Este projeto visa elevar o estado da arte em Harness Engineering, Spec-Driven Development e Multi-Agent Workflows para equipes de desenvolvimento.

## 📋 Índice

- [Código de Conduta](#código-de-conduta)
- [Como Contribuir](#como-contribuir)
- [Reportando Bugs](#reportando-bugs)
- [Sugerindo Melhorias](#sugerindo-melhorias)
- [Pull Requests](#pull-requests)
- [Padrões de Documentação](#padrões-de-documentação)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Desenvolvimento Local](#desenvolvimento-local)

## Código de Conduta

Este projeto segue um código de conduta aberto e inclusivo:

- Seja respeitoso com opiniões e experiências diferentes
- Aceite críticas construtivas de forma graciosa
- Foque no que é melhor para a comunidade e para o projeto
- Demonstre empatia com outros membros da comunidade

## Como Contribuir

Existem várias formas de contribuir:

### 1. Melhorando a Documentação
- Corrigindo erros gramaticais ou de digitação
- Adicionando exemplos práticos de uso
- Traduzindo conteúdo para outros idiomas
- Criando tutoriais e guias adicionais

### 2. Expandindo Templates
- Criando novos templates para domínios específicos
- Melhorando templates existentes com campos adicionais
- Adicionando exemplos de preenchimento

### 3. Aprofundando o Conhecimento
- Adicionando referências acadêmicas e industriais
- Incluindo novos padrões de multi-agent workflows
- Documentando anti-patterns e como evitá-los

### 4. Reportando Problemas
- Bugs na estrutura ou conteúdo
- Inconsistências entre documentos
- Links quebrados ou referências desatualizadas

## Reportando Bugs

Bugs são rastreados como [GitHub Issues](../../issues). Ao reportar um bug, inclua:

- **Título claro e descritivo** do problema
- **Passos para reproduzir** o comportamento
- **Comportamento esperado** vs **comportamento atual**
- **Contexto adicional** (capturas de tela, logs, exemplos)
- **Severidade** (baixa, média, alta, crítica)

### Template de Bug Report

```markdown
## Descrição
[Descreva o bug de forma clara e concisa]

## Passos para Reproduzir
1. [Primeiro passo]
2. [Segundo passo]
3. [etc.]

## Comportamento Esperado
[O que deveria acontecer]

## Comportamento Atual
[O que realmente acontece]

## Contexto Adicional
[Screenshots, logs, exemplos de código]
```

## Sugerindo Melhorias

Melhorias também são rastreadas como [GitHub Issues](../../issues). Ao sugerir uma melhoria:

- Use um título claro e descritivo
- Descreva a motivação por trás da sugestão
- Explique como isso beneficiaria os usuários
- Inclua exemplos de uso se possível

### Áreas de Interesse para Melhorias

- **Novos domínios**: Adicionar bancos de perguntas para domínios não cobertos (IoT, Blockchain, GameDev, etc.)
- **Templates avançados**: Templates para architectures específicas (Event Sourcing, CQRS, Saga Pattern)
- **Integrações**: Guias de integração com ferramentas específicas (Jira, Linear, Notion)
- **Métricas**: Frameworks de medição de qualidade de specs e harnesses
- **Estudos de caso**: Exemplos reais de implementação bem-sucedida

## Pull Requests

### Processo de Submissão

1. **Fork** o repositório
2. **Crie uma branch** para sua feature (`git checkout -b feature/amazing-feature`)
3. **Faça suas alterações** seguindo os padrões do projeto
4. **Commit** suas mudanças (`git commit -m 'feat: add amazing feature'`)
5. **Push** para a branch (`git push origin feature/amazing-feature`)
6. **Abra um Pull Request**

### Convenções de Commit

Usamos [Conventional Commits](https://www.conventionalcommits.org/):

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| `feat` | Nova funcionalidade | `feat: add IoT domain question bank` |
| `fix` | Correção de bug | `fix: correct template reference in SKILL.md` |
| `docs` | Alterações de documentação | `docs: expand SDD maturity section` |
| `style` | Formatação, sem mudança de lógica | `style: fix markdown formatting` |
| `refactor` | Refatoração de código/conteúdo | `refactor: restructure templates directory` |
| `test` | Adição ou correção de testes | `test: add validation for agent-spec template` |
| `chore` | Tarefas de manutenção | `chore: update README badges` |

### Requisitos para Merge

- [ ] O PR descreve claramente o que foi alterado e por quê
- [ ] Todas as mudanças seguem os padrões de documentação do projeto
- [ ] Links internos estão corretos e funcionais
- [ ] Cross-references entre documentos foram atualizadas
- [ ] Exemplos foram testados e validados

## Padrões de Documentação

### Formatação Markdown

- Use **headers hierárquicos** (`#`, `##`, `###`, `####`)
- Prefira **listas** para informações enumeráveis
- Use **tabelas** para dados comparativos
- Inclua **callouts** para informações importantes:

  ```markdown
  > **IMPORTANTE:** Texto de destaque aqui

  > **DICA:** Texto de dica aqui

  > **ATENÇÃO:** Texto de aviso aqui
  ```

### Referências Cruzadas

- Use links relativos para documentos internos: `[SKILL.md](./SKILL.md)`
- Referencie seções específicas: `[Seção 3.2](./SKILL.md#32-sensores)`
- Mantenha consistência nos nomes de arquivos: `KEBAB-CASE.md`

### Estrutura de Templates

Todos os templates devem seguir:

```markdown
# Template: Nome do Template

> **Objetivo:** [Descrição clara do propósito]
> **Quando usar:** [Contextos de aplicação]
> **Nível SDD:** [L1/L2/L3]

## Instruções de Preenchimento

1. [Instrução passo a passo]
2. [etc.]

## Template

[Estrutura do template com placeholders]

## Exemplo Preenchido

[Exemplo concreto de uso]
```

## Estrutura do Projeto

```
harness-copilot-skill/
├── SKILL.md                 # Guia principal da skill
├── AGENTS.md                # Instruções permanentes para agentes
├── INTERACTIVE.md           # Protocolo de descoberta interativa
├── QUICKSTART.md            # Guia de início rápido
├── README.md                # Documentação principal
├── CONTRIBUTING.md          # Este arquivo
├── LICENSE                  # Licença MIT
├── .github/
│   └── copilot-instructions.md  # Configuração GitHub Copilot
├── templates/               # Templates reutilizáveis
│   ├── sdd-requirements.md
│   ├── sdd-design.md
│   ├── sdd-tasks.md
│   ├── harness-sensors.md
│   ├── data-contract.md
│   ├── agent-spec.md
│   ├── multi-agent-workflow.md
│   └── DISCOVERY-OUTPUT.md
└── examples/                # Exemplos práticos
    ├── nivel1-basic-chatbot/
    ├── nivel2-microservice/
    ├── nivel3-distributed-system/
    ├── data-pipeline-autohealing/
    └── sessao-interativa/
```

## Desenvolvimento Local

### Pré-requisitos

- Git instalado
- Editor de texto com suporte a Markdown
- GitHub Copilot (opcional, para testar a skill)

### Testando a Skill

1. Copie os arquivos para `.github/` ou `.github/copilot-instructions.md` no seu repositório
2. Adicione `SKILL.md` e `AGENTS.md` na raiz ou em `.opencode/agent/`
3. Abra um issue ou PR e interaja com o GitHub Copilot
4. Use o protocolo interativo descrito em `INTERACTIVE.md`

### Validação de Links

Para verificar links quebrados:

```bash
# Usando markdown-link-check
npm install -g markdown-link-check
find . -name "*.md" -exec markdown-link-check {} \;
```

### Preview da Documentação

Use extensões como **Markdown Preview** no VS Code para visualizar a renderização.

## 📞 Contato

- **Issues**: [Abra uma issue](../../issues)
- **Discussions**: [Participe das discussões](../../discussions)
- **Autor**: [o-lino](https://github.com/o-lino)

## 🙏 Agradecimentos

Este projeto é baseado em pesquisa extensiva de:

- **Harness Components** (Guides + Sensors) — Böckeler & Schmolitzky
- **Spec-Driven Development** — Anthropic, OpenAI
- **Multi-Agent Workflows** — Padrões de orquestração enterprise
- **Data Consulting** — Frameworks de descoberta profunda

Obrigado a todos os contribuidores que ajudam a elevar o estado da arte em engenharia de software assistida por IA!

---

> "A qualidade de uma spec determina o teto de qualidade da implementação."
