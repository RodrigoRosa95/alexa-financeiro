# Skill Alexa "financeiro" (pt-BR)

Lança gastos por voz: *"Alexa, pede pro financeiro paguei 30 reais no mercado com pix"*.

A Alexa manda a frase transcrita para `POST /api/alexa` do seu sistema financeiro. A frase é interpretada por IA (com regras fixas de reserva), a forma de pagamento sai da frase ou do histórico, e a Alexa **confirma em voz alta antes de gravar**.

## Segurança
Cada pedido é validado como a Amazon exige para endpoints próprios: certificado `echo-api.amazon.com` com cadeia até raiz confiável, assinatura SHA-256 do corpo bruto, horário de no máximo 150 s e `applicationId` igual a `ALEXA_SKILL_ID`.

## Arquivos
- `alexa-financeiro.js` — verificação de assinatura, interpretação da frase e fluxo de confirmação. As funções do seu sistema (`addTransaction`, `interpretarFraseComIA`, `saldoVale`…) entram por injeção de dependências em `criarSkillAlexa(dep)`.
- `modelos/financeiro-pt-BR.json` — modelo de interação (invocação "financeiro"). Ajuste os nomes das formas de pagamento (slot) aos seus.

## Configuração
`ALEXA_SKILL_ID=amzn1.ask.skill.…` e, opcionalmente, `ALEXA_USUARIOS` (ids de conta Amazon aceitos). Endpoint HTTPS com certificado válido.

Licença MIT.
