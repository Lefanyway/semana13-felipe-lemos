# Integração Contínua em QA

**Aluno:** Felipe Lemos de Moura  
**Disciplina:** Software Testing & Quality Assurance  
**Atividade:** Semana 13 — Módulo 3 — Prof. Raphael Botelho

## Tabela de conceitos

| Conceito | O que é em uma frase |
| --- | --- |
| DevOps | Cultura de colaboração entre desenvolvimento e operações para entregar e manter software com automação, feedback e qualidade contínua. |
| Integração Contínua (CI) | Prática de integrar alterações frequentemente e executar verificações automáticas para detectar problemas de integração cedo. |
| Entrega/Implantação Contínua (CD) | Na entrega contínua, o código validado fica pronto para publicação mediante aprovação; na implantação contínua, a publicação em produção também ocorre automaticamente. |
| Pipeline | Sequência automatizada de atividades, como obter o código, instalar dependências, executar testes e, quando previsto, publicar a aplicação. |
| Workflow | Processo automatizado do GitHub Actions definido em um arquivo YAML dentro de `.github/workflows`. |
| Job e Step | Um job agrupa etapas executadas em um runner; cada step executa um comando ou uma action, normalmente em sequência dentro desse job. |
| Runner | Ambiente que executa os jobs do workflow, como a máquina virtual disponibilizada pelo GitHub com `ubuntu-latest`. |
| Gatilho (trigger) | Evento que inicia um workflow, como `push`, `pull_request` ou execução manual com `workflow_dispatch`. |
| Modo headless | Execução de um navegador sem exibir sua interface gráfica, mantendo a capacidade de interagir com páginas e executar testes. |
| YAML | Formato de texto usado para descrever configurações estruturadas, com indentação por espaços que delimita blocos. |

## 1. Qual o papel do QA no DevOps?

O QA participa desde o planejamento, ajudando a definir critérios de aceitação, riscos e cenários de teste. Ele automatiza verificações de API e interface, integra essas verificações ao pipeline e define com o time quais falhas impedem uma entrega. Também analisa os resultados, investiga falhas e comunica os problemas para que sejam corrigidos cedo. Assim, a qualidade é acompanhada durante todo o desenvolvimento.

## 2. Por que rodar os testes automaticamente a cada integração de código (push)?

Executar os testes a cada push fornece feedback rápido e permite identificar regressões próximas da alteração que as causou. A execução automática reduz a dependência de alguém lembrar de testar e padroniza as verificações em um ambiente preparado pelo pipeline. Se uma asserção falhar, o Newman retorna um código de saída diferente de zero e o job fica vermelho. Esse resultado pode ser usado para bloquear o merge ou a implantação quando essas regras estiverem configuradas; um workflow vermelho sozinho não impede novos pushes.

## 3. O que é o modo headless e por que ele é usado no CI?

Headless é executar o navegador sem mostrar uma janela gráfica. Os testes continuam podendo abrir páginas, preencher campos, clicar e validar resultados. Esse modo é apropriado para runners de CI, que normalmente não têm uma sessão gráfica interativa, e permite automatizar a execução sem intervenção humana. No Cypress, `npx cypress run` roda em headless por padrão; `npx cypress open` abre a interface para desenvolvimento e depuração. Newman executa testes HTTP de API e não precisa de navegador.

## Referências

- Material da Semana 13, Prof. Raphael Botelho, fornecido na disciplina.
- [GitHub Actions — conceitos fundamentais](https://docs.github.com/pt/actions/get-started/understand-github-actions).
- [Cypress — comandos de linha de comando](https://docs.cypress.io/app/references/command-line).
- [Newman — documentação oficial](https://github.com/postmanlabs/newman).
