# Automação do formulário — CashewCare

Quando alguém preenche o formulário do site:
1. o contato é salvo numa planilha Google ("Leads CashewCare");
2. a pessoa recebe um e-mail de **cashewcarecontato@gmail.com** com a logo do caju, um convite para mandar perguntas e o link do Instagram **@cashewcareoficial**;
3. a equipe recebe um aviso no mesmo e-mail (dá pra responder direto pra pessoa).

Custo: zero (Google Apps Script). Limite do Gmail gratuito: ~100 e-mails/dia.

## Configuração (uns 10 minutos, uma vez só)

> Faça tudo **logado na conta cashewcarecontato@gmail.com** — é ela que aparece como remetente.

1. Acesse https://script.google.com → **Novo projeto**. Renomeie para "Formulário CashewCare".
2. Apague o conteúdo de `Código.gs` e cole **todo** o conteúdo do arquivo `Code.gs` desta pasta. Salve (Ctrl+S).
3. No menu de funções lá em cima, escolha **testar** → **Executar**.
   - O Google vai pedir autorização: *Revisar permissões* → escolha a conta → *Avançado* → *Acessar Formulário CashewCare (não seguro)* → *Permitir*. (Aparece "não seguro" porque o script é seu e não passou por verificação do Google — é normal.)
   - Confira a caixa de entrada de cashewcarecontato@gmail.com: devem chegar o e-mail de boas-vindas e o aviso de novo contato. A planilha "Leads CashewCare" aparece no Drive.
4. **Implantar** → **Nova implantação** → engrenagem → **App da Web**.
   - Executar como: **Eu (cashewcarecontato@gmail.com)**
   - Quem pode acessar: **Qualquer pessoa**
   - Clique em **Implantar** e copie a **URL do app da Web** (termina em `/exec`).
5. No `index.html`, procure por `const FORM_ENDPOINT = '';` e cole a URL entre as aspas:
   ```js
   const FORM_ENDPOINT = 'https://script.google.com/macros/s/XXXXXXXX/exec';
   ```
6. Publique o site de novo e faça um envio de teste pelo próprio formulário.

## Se precisar mudar algo depois
- Texto do e-mail: função `sendWelcome_` no `Code.gs`.
- Desligar o aviso para a equipe: `NOTIFY_TEAM: false`.
- Depois de editar o script, vá em **Implantar → Gerenciar implantações → editar (lápis) → Versão: Nova versão → Implantar**. A URL continua a mesma.
