# Projeto de Testes de API - JSONPlaceholder

Este repositório contém uma coleção de testes de API criados no Postman e preparados para execução local e em CI.

**Visão geral**
- Coleção Postman: `Jsonplaceholder-ci.json` (nome da coleção: "Jsonplaceholder").
- Ambiente Postman: `Jsonplaceholder-env.json` (variável `BASE_URL` apontando para https://jsonplaceholder.typicode.com/).
- Objetivo: validar respostas e contrato (JSON Schema) de endpoints públicos do JSONPlaceholder.

**Endpoints testados**
- `GET /posts` — lista todos os posts.
- `GET /posts/1` — obtém o post com id 1.
- `GET /posts/1/comments` — lista comentários do post 1.
- `GET /comments?postId=1` — lista comentários filtrados por `postId=1`.

**O que os testes validam**
- Status code 200 para respostas bem-sucedidas.
- Contrato (JSON Schema) para objetos de `post` e `comment` usando a biblioteca Ajv nos scripts de teste do Postman.

**Requisitos**
- Postman (importar coleção e ambiente) — para execução manual.
- Node.js + npm — para instalar o Newman (executor CLI do Postman) quando executar via linha de comando ou CI.

**Como executar localmente**

1) Execução via Postman (GUI):
- Importe `Jsonplaceholder-ci.json` como coleção e `Jsonplaceholder-env.json` como ambiente.
- Selecione o ambiente "Jsonplaceholder" e execute a coleção ou as requisições desejadas.

2) Execução via Newman (linha de comando):

Instale o Newman globalmente (se necessário):
```bash
npm install -g newman
```

Execute a coleção com o ambiente fornecido:
```bash
newman run Jsonplaceholder-ci.json -e Jsonplaceholder-env.json
```

Opcional: gerar relatório HTML
```bash
newman run Jsonplaceholder-ci.json -e Jsonplaceholder-env.json --reporters cli,html --reporter-html-export report.html
```

**Integração em CI**
- A coleção `Jsonplaceholder-ci.json` foi exportada para uso em pipelines. Em CI, basta executar o comando do Newman acima. O comando retorna código de saída diferente de zero quando algum teste falha, permitindo falhar o build.

**Observações técnicas**
- Os scripts de teste utilizam `Ajv` (disponível no ambiente de execução do Postman) para validação de JSON Schema.
- A variável `BASE_URL` está definida em `Jsonplaceholder-env.json` como `https://jsonplaceholder.typicode.com/`.

