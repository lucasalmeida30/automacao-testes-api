# **Testes Automatizados da API ServeRest**

## **Introdução**

Este repositório contém testes automatizados para a API **ServeRest**, cobrindo os seguintes endpoints:

- **GET /usuarios**: Retorna uma lista de todos os usuários.
- **POST /usuarios**: Cria um novo usuário.
- **GET /usuarios/{id}**: Retorna os detalhes de um usuário específico.
- **PUT /usuarios/{id}**: Atualiza as informações de um usuário.
- **DELETE /usuarios/{id}**: Exclui um usuário.

Os testes foram implementados utilizando **Postman** e executados via **Newman**, sendo integrados a pipelines CI/CD.

---

## **Requisitos**

Antes de rodar os testes, certifique-se de ter os seguintes requisitos instalados:

- [Node.js](https://nodejs.org/) (versão LTS recomendada)
- [Newman](https://www.npmjs.com/package/newman): CLI para executar collections do Postman
- [newman-reporter-htmlextra](https://www.npmjs.com/package/newman-reporter-htmlextra): Gerador de relatórios HTML detalhados

Para instalar os pacotes necessários, execute:

```sh
npm install -g newman newman-reporter-htmlextra
```

---

## **Casos de Teste Cobertos**

### **1. GET /usuarios - Listar Usuários**

✅ **Testes Implementados:**

- Verificar se a resposta retorna **código 200**.
- Verificar se o corpo da resposta é um **Objeto**.
- Verificar se os objetos contêm as propiedades esperadas(`quantidade`, `usuarios`).
- Verificar se os campos da resposta nao estão vazios.

### **2. POST /usuarios - Criar Usuário**

✅ **Testes Implementados:**

- Verificar se a resposta retorna **código 201** para uma criação bem-sucedida.
- Validar se a resposta contém a mensagem esperada.
- Validar que um **e-mail inválido** retorna erro 400.
- Testar a criação sem um campo obrigatório (`nome` ou `email`).

### **3. GET /usuarios/{id} - Obter um Usuário Específico**

✅ **Testes Implementados:**

- Verificar se a resposta retorna **código 200** para um ID válido.
- Validar que o objeto retornado contém `_id`, `nome`, `email`, `password`, `administrador`.
- Validar que um **usuário inexistente** retorna **erro 400**.

### **4. PUT /usuarios/{id} - Atualizar um Usuário**

✅ **Testes Implementados:**

- Verificar se a resposta retorna **código 200** após uma atualização bem-sucedida.
- Validar que um **usuário inexistente** retorna erro **400**.
- Testar a tentativa de atualizar sem a propiedade **e-mail**.

### **5. DELETE /usuarios/{id} - Excluir um Usuário**

✅ **Testes Implementados:**

- Verificar se a resposta retorna **código 200** após uma exclusão bem-sucedida.
- Validar que um **usuário inexistente** retorna mensagem  **Nenhum registro excluído**.

---

## **Como Rodar os Testes**

### **1. Executar os testes manualmente no Postman**

1. Importe a collection do Postman (`test-qa1.json`).
2. Configure o ambiente com os valores adequados (`test-environment.json`).
3. Execute os testes manualmente.

### **2. Executar os testes automaticamente via Newman**

Para rodar os testes automatizados via Newman, utilize o seguinte comando:

```sh
newman run test-qa1.json -g test-environment.json --delay-request 1 --reporters cli, -r htmlextra --reporter-htmlextra-export ./result/Report.html
```

---

## **Conclusão**

Os testes cobrem os principais cenários dos endpoints de usuários da API **ServeRest**, garantindo sua confiabilidade. Além disso, a automação gera um **relatório HTML detalhado** utilizando **newman-reporter-htmlextra**, facilitando a análise dos resultados. Para qualquer dúvida ou sugestão, entre em contato comigo. 🚀
