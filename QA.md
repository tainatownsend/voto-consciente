# QA — protótipo Voto Consciente

Este arquivo acompanha o que pode avançar sem alterar a direção visual/pedagógica aprovada e o que deve aguardar validação humana.

## Concluído

- [x] Repositório público criado e PR de protótipo aberta.
- [x] GitHub Pages configurado via GitHub Actions na branch do protótipo.
- [x] Workflow de Pages alinhado às versões atuais recomendadas pelo GitHub.
- [x] Estrutura mobile-first.
- [x] Uma ideia principal e uma ação principal por tela.
- [x] Navegação compatível com o botão Voltar do navegador.
- [x] Recarregar uma URL `#passo-N` preserva a etapa atual em vez de reiniciar a jornada.
- [x] Foco de teclado movido para o título ao trocar de etapa.
- [x] Suporte a `prefers-reduced-motion`.
- [x] Ilustração da Dona Antonia separada como asset.
- [x] Conteúdo eleitoral principal revisado com referência ao TSE.
- [x] Contraste das combinações principais revisado: texto, verde institucional, botão e caixas de destaque passam com folga o nível AA para texto normal.
- [x] Textos alternativos principais revisados; ilustrações repetidas/decorativas podem ficar com `alt` vazio.

## QA técnico que pode continuar sem mudar a experiência aprovada

- [ ] Confirmar deploy público do GitHub Pages.
- [ ] Testar ausência de rolagem horizontal em 320 px, 375 px, 390 px, tablet e desktop.
- [ ] Testar navegação completa apenas por teclado em navegador real.
- [ ] Validar Voltar/Avançar e recarregamento em navegador real após a correção de estado por hash.
- [ ] Testar experiência com movimento reduzido em navegador real.
- [ ] Testar carregamento em conexão lenta.
- [ ] Verificar HTML e links quebrados.

## Aguardando validação da experiência

- [ ] A Home deixa claro, sem explicação prévia, onde clicar primeiro?
- [ ] A primeira pílula parece curta e leve?
- [ ] Cada tela apresenta informação suficiente sem sobrecarregar?
- [ ] A linguagem parece simples sem infantilizar?
- [ ] Dona Antonia funciona como companheira da jornada, e não como professora?
- [ ] O usuário percebe naturalmente qual é o próximo passo?
- [ ] O visual da personagem está próximo o suficiente da referência aprovada?

## Depois da validação

- [ ] Incorporar feedback da primeira rodada de uso.
- [ ] Fazer QA final de conteúdo e acessibilidade.
- [ ] Decidir se a PR pode ser incorporada à `main`.
- [ ] Só então expandir as próximas trilhas de aprendizagem.
