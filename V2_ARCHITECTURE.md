# Voto Consciente — V2 “Próximo Degrau”

## Princípio central

A pessoa não precisa entender a arquitetura do site. Ela precisa entender **o que fazer agora**.

Regra de cada tela:

> **1 ideia principal → 1 recurso visual → 1 ação principal**

Teste obrigatório de conteúdo e UX:

> “Uma pessoa de 75 anos, com baixo nível de alfabetização e pouca familiaridade com tecnologia, conseguiria entender esta tela e saber exatamente onde tocar sem ajuda?”

Se a resposta não for um “sim” seguro, a tela precisa ser simplificada.

## Home

**Objetivo:** explicar rapidamente o valor do site e deixar apenas um caminho ativo.

**Mensagem principal:**

- “Vamos entender seu voto?”
- “Política explicada de um jeito simples. Uma coisa de cada vez.”

**Formas de aprender:**

- **Ler — disponível agora**
- **Ouvir — em breve**
- **Assistir — em breve**

Somente “Ler” está disponível. As outras duas opções aparecem como futuras, sem parecer botões quebrados.

**Ação principal:** `COMEÇAR A LER`

## Jornada eleitoral — 8 passos

### Passo 1 — Antes do nome, entenda o trabalho

**Ideia:** cargo é um trabalho.

**Analogia:** cano quebrado → pessoa que entende de cano; problema elétrico → pessoa que entende de eletricidade.

**Frase para guardar:** “Primeiro entenda o cargo. Depois escolha a pessoa.”

### Passo 2 — Na política, existem trabalhos diferentes

**Ideia:** nesta eleição, há dois grandes tipos de trabalho que precisamos entender primeiro.

- Presidente e Governador: administrar o governo.
- Deputados e Senadores: fazer e mudar leis e acompanhar o governo.

O termo “fiscalizar” só aparece **depois** da explicação simples.

**Frase para guardar:** “Um cargo não faz o trabalho do outro.”

### Passo 3 — Na urna, serão seis escolhas

Ordem oficial das Eleições Gerais de 2026:

1. Deputado Federal
2. Deputado Estadual ou Distrital
3. Senador — primeira escolha
4. Senador — segunda escolha
5. Governador
6. Presidente

**Frase para guardar:** “São seis escolhas. Duas são para senador.”

### Passo 4 — O candidato fez uma promessa

**Pergunta ensinada:** “Isso faz parte do trabalho desse cargo?”

A analogia do trabalho é retomada: não adianta pedir ao eletricista o trabalho do encanador.

**Frase para guardar:** “Pergunte: esse cargo pode fazer isso?”

### Passo 5 — A promessa parece boa. Como vai acontecer?

Duas perguntas simples:

- Como vai fazer?
- De onde vem o dinheiro?

**Frase para guardar:** “Promessa boa precisa de explicação.”

### Passo 6 — Quem está pedindo seu voto?

Perguntas simples:

- O que essa pessoa já fez?
- O que ela fala combina com o que já fez?
- Onde posso conferir informações sobre ela?

**Frase para guardar:** “Procure saber antes de decidir.”

### Passo 7 — Chegou uma mensagem no celular. É verdade?

Rotina curta:

1. **PARE** — não passe adiante na hora.
2. **VEJA** — quem publicou?
3. **CONFIRA** — outro lugar confiável diz a mesma coisa?

**Frase para guardar:** “PARE. VEJA. CONFIRA.”

### Passo 8 — Agora você sabe o que perguntar

Checklist final:

- Sei qual é o trabalho do cargo?
- A promessa cabe nesse trabalho?
- Entendi como pretende fazer?
- Procurei conhecer melhor a pessoa?
- Conferi as informações importantes?

**Fechamento:** “O voto é seu. A escolha também.”

## Tela de conclusão

Não abre imediatamente novas trilhas. Primeiro dá sensação de encerramento:

- “Pronto. Você deu seu primeiro passo.”
- “Você não precisa saber tudo sobre política para escolher melhor.”

As próximas trilhas são anunciadas apenas como futuras.

## Direção visual

- Dona Antonia permanece como personagem-guia.
- Cada passo recebe uma ilustração que ajuda a explicar a ideia; não apenas decoração.
- Poucas cores por tela.
- Tipografia grande e alto contraste.
- Botões grandes, com uma ação principal clara.
- Sem menus complexos durante a jornada.

## Responsividade

Prioridade: celular.

Regras implementadas:

- nenhuma largura fixa maior que a viewport;
- `overflow-x: hidden` em página;
- imagens e SVGs limitados a `max-width: 100%`;
- alvos de toque grandes;
- coluna única para evitar decisões de layout em telas pequenas;
- conteúdo limitado a uma largura confortável em tablet e desktop;
- suporte a `prefers-reduced-motion`;
- foco visível para navegação por teclado;
- progresso textual: “Passo X de 8”, além da barra visual.

## Confiança e neutralidade

O rodapé usa linguagem direta:

> “Este projeto não apoia partido nem candidato. Queremos ajudar você a entender melhor a política e fazer suas próprias escolhas.”

As informações específicas das Eleições 2026 são conferidas em fontes oficiais do Tribunal Superior Eleitoral (TSE).
