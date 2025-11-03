# Histórico de Alterações

### Implementação de Expiração de Links
**Objetivo:** Permitir que os links encurtados tenham uma data de expiração.

**Plano:**
1.  Modificar o `urlSchema` para incluir um campo `expires_at`.
2.  Atualizar o endpoint `POST /shorten` para aceitar e salvar a data de expiração.
3.  Atualizar o endpoint `GET /:shortCode` para verificar a expiração do link.

**Alterações Realizadas:**
-   **2025-11-03:** Adicionado o campo `expires_at` (tipo `Date`, opcional) ao `urlSchema` em `server.js`.
-   **2025-11-03:** Modificado o endpoint `POST /shorten` em `server.js` para aceitar o parâmetro `expires_in` (ex: '1h', '7d'), calcular `expires_at` e salvá-lo no banco de dados. Adicionada a função auxiliar `parseExpiration`.
-   **2025-11-03:** Modificado o endpoint `GET /:shortCode` em `server.js` para verificar se o link expirou. Se expirado, retorna status 410 (Gone) com mensagem de erro.
-   **2025-11-03:** Adicionado suporte para minutos ('m') na função `parseExpiration` em `server.js`.
-   **2025-11-03:** Modificado o endpoint `POST /shorten` em `server.js` para garantir que `expires_at` seja sempre definido. Se `expires_in` não for fornecido, um padrão de 1 minuto de expiração é aplicado.
