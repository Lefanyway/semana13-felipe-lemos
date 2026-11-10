# Semana 13 — Integração Contínua em QA

**Aluno:** Felipe Lemos de Moura  
**Professor:** Raphael Botelho  
**Módulo 3:** Automação de Testes

Este projeto executa a coleção Postman da aula com Newman e GitHub Actions para detectar falhas a cada alteração de código.

## Executar localmente

Instale Node.js 24 e execute na pasta do projeto:

```sh
npm ci
npm test
```

Também é possível importar `colecao.json` no Postman. A coleção usa a API pública JSONPlaceholder e não requer token nem senha.

## Cenários

| Requisição | Resultado esperado |
| --- | --- |
| `GET /users/1` | HTTP 200, id 1, nome Leanne Graham e corpo compatível com o JSON Schema da aula. |
| `GET /users/9999` | HTTP 404 para usuário inexistente. |
| `POST /posts` | HTTP 201 e título igual ao enviado. |

API: `https://jsonplaceholder.typicode.com`. A criação de posts é simulada pelo serviço e não persiste os dados.

## Pipeline

O arquivo `.github/workflows/main.yml` contém o workflow **Testes de API**, acionado por push, pull request e pelo botão **Run workflow**. O job `testes-api` usa `ubuntu-latest`, obtém o repositório, prepara Node.js, instala as dependências com `npm ci` e executa `npm test`.

Qualquer falha de teste retorna erro e deixa o job vermelho. Para impedir merges ou implantações automaticamente, é necessário configurar também as regras correspondentes do repositório ou os jobs de implantação.

Os relatórios JSON e JUnit XML são gerados em `relatorios/`. No GitHub Actions, o passo final tenta armazená-los como artefato **relatorios-newman**, inclusive em caso de falha dos testes, por 30 dias.

## Missão 4

1. Altere apenas a asserção de status do primeiro cenário de `200` para `201` e faça commit.
2. Na aba Actions, confira que o cenário recebeu 200 e falhou porque esperava 201.
3. Restaure o esperado para `200`, faça novo commit e confira o resultado verde.
4. Acrescente um teste que valide o `userId` do post criado e faça novo commit.

Cada etapa deve gerar sua própria execução no GitHub. Execuções locais são verificações complementares e não substituem a evidência do Actions.

## Arquivos

- `colecao.json`: coleção da aula e testes.
- `.github/workflows/main.yml`: pipeline e armazenamento de relatórios.
- `TEORIA.md`: tabela de conceitos e respostas às três perguntas.
- `package.json` e `package-lock.json`: instalação reproduzível do Newman.

## Fontes técnicas

- [Newman](https://github.com/postmanlabs/newman)
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/)
- [GitHub Actions](https://docs.github.com/pt/actions/get-started/understand-github-actions)
- [Checkout](https://github.com/actions/checkout), [Setup Node](https://github.com/actions/setup-node) e [Upload Artifact](https://github.com/actions/upload-artifact)
