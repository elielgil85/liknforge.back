# Projeto: backend_liknforge

## 1. Descrição do Projeto
Este projeto é o backend da aplicação, responsável por [Adicionar descrição do projeto aqui].

## 2. Instruções de Configuração
Para configurar e rodar o projeto localmente:

1.  **Instalar Dependências:**
    ```bash
    npm install
    ```
2.  **Configurar Variáveis de Ambiente:**
    Crie um arquivo `.env` na raiz do projeto e adicione as variáveis necessárias (veja a seção "Variáveis de Ambiente" abaixo).

3.  **Iniciar o Servidor:**
    ```bash
    npm start
    ```

## 3. Tecnologias Chave
-   Node.js
-   Express.js (presumido, verificar `server.js`)
-   [Adicionar outras tecnologias/bibliotecas aqui]

## 4. Endpoints da API

### 1. Encurtar URL

*   **Endpoint:** `POST /shorten`
*   **Funcionalidade:** Cria uma URL curta para uma URL longa fornecida.
*   **Corpo da Requisição (JSON):**
    ```json
    {
      "long_url": "https://sua-url-longa-aqui.com",
      "expires_in": "7d" // Opcional: tempo de expiração (ex: "1h" para 1 hora, "7d" para 7 dias)
    }
    ```
*   **Resposta de Sucesso (201 Created):**
    ```json
    {
      "short_code": "aB1cD2e",
      "expires_at": "2025-11-10T12:00:00.000Z" // Presente se expires_in foi fornecido
    }
    ```
*   **Resposta de Erro (400 Bad Request):** Se a `long_url` for inválida.

### 2. Obter URL Longa para Redirecionamento

*   **Endpoint:** `GET /:shortCode` (onde `:shortCode` é o código do link)
*   **Funcionalidade:** Busca a URL longa original associada a um código curto.
*   **Parâmetro de URL:** O `shortCode` gerado pela rota `/shorten`.
*   **Resposta de Sucesso (200 OK):**
    ```json
    {
      "long_url": "https://sua-url-longa-aqui.com"
    }
    ```
*   **Resposta de Erro (404 Not Found):** Se o `shortCode` não for encontrado.
    ```json
    {
      "error": "Short URL not found."
    }
    ```
*   **Resposta de Erro (410 Gone):** Se o link estiver expirado.
    ```json
    {
      "error": "Short URL has expired."
    }
    ```

---

**Observação Importante:** O frontend Next.js utiliza um proxy (`next.config.ts`) que reescreve requisições de `/api/backend/*` para o servidor backend rodando em `http://localhost:3001/*`. Portanto, o backend deve estar acessível nessa porta e responder a essas rotas diretamente (sem o prefixo `/api/backend`).

## 5. Variáveis de Ambiente
As seguintes variáveis de ambiente são necessárias no arquivo `.env`:
-   `PORT`: Porta em que o servidor irá rodar (ex: `PORT=3001`)
-   `MONGODB_URI`: URI de conexão com o MongoDB Atlas.
-   [Adicionar outras variáveis de ambiente aqui]

## 6. Scripts
-   `npm start`: Inicia o servidor da aplicação.
-   [Adicionar outros scripts npm aqui, ex: `npm test`]

## 7. Histórico de Alterações
Para um histórico detalhado das alterações, consulte [CHANGELOG.md](CHANGELOG.md).
