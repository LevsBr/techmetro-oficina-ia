# PROMPTS — ROTA A · Campus Events

**Tech Metro · Unifametro — Do Zero ao Projeto: Engenharia de Prompts na Prática**

Mediador: Levi Celestino Azevedo Pereira · Apoio: Ariel Barbosa e Josué Silva

> Todos os prompts abaixo estão prontos para copiar e colar em qualquer assistente de IA de texto (ex.: Claude, ChatGPT, Gemini). O método **P.A.C.T.O.** é material da equipe.
> Os eventos usados são **fictícios** — não representam a programação oficial da universidade.

Materiais relacionados: [Guia do Participante](../materiais/TechMetro_Guia_do_Participante.md) · [Slides](../materiais/TechMetro_Slides.pdf) · [Demonstração Campus Events](../index.html) · [Página inicial do repositório](../README.md)

---

## Fluxo da oficina

**Ideia → Contexto → Requisitos → Prompt → Código → Teste → Revisão**

---

## P0 — Prompt vago (demonstração do erro)

```text
Faz um site de eventos da faculdade.
```

**Por que falha?** A IA precisa adivinhar: quem usa, quais dados cada evento tem, se precisa de busca, qual linguagem, quantos arquivos, como é o visual, se deve funcionar no celular e como saber se ficou "pronto". O resultado tende a ser genérico, incompleto ou difícil de executar.

---

## P1 — Levantamento de requisitos (antes de pedir código)

```text
Atue como analista de requisitos de software.
Tenho a ideia de um site simples para estudantes encontrarem eventos do campus.
Antes de escrever qualquer código, liste em Markdown:
1. Requisitos funcionais (no máximo 6).
2. Requisitos não funcionais (no máximo 4).
3. Três perguntas que você faria ao cliente para eliminar ambiguidades.
Seja objetivo: uma linha por item.
```

---

## P2 — Prompt estruturado com P.A.C.T.O. + Markdown + XML (prompt principal)

```text
# P — Persona
Atue como desenvolvedor front-end sênior especializado em acessibilidade.

# A — Ação
Crie o aplicativo web "Campus Events" para divulgação de eventos universitários.

# C — Contexto & Estilo
<contexto>
Público: estudantes universitários, acessando pelo celular e pelo notebook.
Use somente eventos FICTÍCIOS (6 eventos), com: título, categoria, data, horário, local e descrição.
Categorias: Workshop, Palestra, Competição.
</contexto>

<requisitos>
- Título e identificação da plataforma no topo.
- Eventos exibidos em cards.
- Campo de busca por título, local ou descrição, ignorando acentos e maiúsculas.
- Mensagem clara quando nenhum evento corresponder à busca.
- Layout responsivo (celular e desktop).
- Acessível: labels nos campos, foco visível por teclado, bom contraste.
</requisitos>

<restricoes>
- HTML, CSS e JavaScript em UM ÚNICO arquivo .html.
- Sem bibliotecas, frameworks, CDN ou servidor.
- Inserir textos com textContent (não usar innerHTML com dados).
</restricoes>

# T — Tom / Atmosfera
Visual moderno e tecnológico: fundo escuro, detalhes em azul, ciano e roxo. Código limpo e comentado em português.

# O — Output
Entregue apenas o código completo do arquivo em um bloco de código, seguido de uma lista curta (máx. 5 itens) explicando como testar.
```

---

## P3 — Few-shot: ensinando o formato do dado por exemplo

```text
Gere mais 3 eventos fictícios seguindo EXATAMENTE o formato dos exemplos.

Exemplo 1:
{ titulo: "Introdução ao Python", categoria: "Workshop", data: "2026-11-03", hora: "19:00", local: "Laboratório 2", descricao: "Primeiros passos com variáveis, listas e laços em Python." }

Exemplo 2:
{ titulo: "Carreira em Tecnologia", categoria: "Palestra", data: "2026-11-05", hora: "10:00", local: "Auditório Central", descricao: "Como montar portfólio e se preparar para o primeiro estágio." }

Responda somente com os 3 objetos, um por linha.
```

**Comparação zero-shot:** “Gere 3 eventos para o site.” → a IA escolhe campos, formato e tamanho por conta própria (pode vir em tabela, em texto corrido ou com campos diferentes).

> **Atenção:** os exemplos do P3 estão no formato de **objeto literal JavaScript** (nomes das propriedades sem aspas), o mesmo usado dentro do `index.html`. Eles **não são JSON válido**. Para obter JSON, coloque os nomes das propriedades entre aspas duplas nos exemplos e peça explicitamente: “responda em JSON válido”. Veja o capítulo 4 do Guia do Participante.

---

## P4 — Reasoning Process: plano de solução verificável

```text
Antes de gerar o código do Campus Events, apresente um plano de implementação:
- de 4 a 6 etapas numeradas;
- para cada etapa, uma justificativa de no máximo uma linha;
- para cada etapa, como eu posso verificar que ela funcionou.
Não escreva código ainda.
```

> Observação didática: pedimos um **plano com etapas verificáveis**, não o "raciocínio interno" do modelo. O plano é uma resposta como outra qualquer — e também deve ser conferido.

---

## P5 — Success Criteria: critérios objetivos de aceite

```text
Considere o Campus Events pronto somente se TODOS os critérios forem atendidos:
1. Abre com duplo clique no navegador, sem internet e sem servidor.
2. Exibe 6 cards com título, data, horário, local e descrição.
3. Buscar "logica" (sem acento) encontra "Maratona de Lógica".
4. Buscar "robótica" mostra a mensagem "Nenhum evento encontrado".
5. Em tela de 390 px de largura não há rolagem horizontal.
6. É possível chegar ao campo de busca usando apenas a tecla Tab.
Verifique o seu código contra cada critério e responda com uma tabela: Critério | Atende? | Evidência no código.
```

---

## P6 — Self-Criticism Task: autocrítica e correção

```text
Revise criticamente o código que você gerou como se fosse um revisor de código exigente.
Liste até 5 problemas, cada um com: severidade (alta/média/baixa), onde está e como corrigir.
Considere: acessibilidade, responsividade, segurança (uso de innerHTML), legibilidade e requisitos não atendidos.
Depois, entregue o arquivo completo já corrigido.
```

---

## P7 — Melhoria guiada por prompt (refinamento)

```text
Agora melhore o Campus Events sem quebrar o que já funciona:
1. Adicione um filtro por categoria (select com "Todas", Workshop, Palestra, Competição) que funcione junto com a busca.
2. Mostre um contador acessível: "X de Y eventos exibidos" (use aria-live="polite").
3. Na mensagem de "nenhum evento", inclua um botão "Limpar filtros" que restaura a lista e devolve o foco à busca.
Mantenha arquivo único e sem dependências. Entregue o arquivo completo.
```

---

## Prompts reserva (se sobrar tempo ou para a turma testar depois)

```text
Ordene os cards por data, do mais próximo para o mais distante, e destaque visualmente o próximo evento com o selo "Em breve".
```

```text
Explique este código para um calouro de ADS em 5 tópicos curtos, sem jargões desnecessários.
```

---

## Contingência

Se a IA demorar, falhar ou a internet cair: abrir o **[index.html](../index.html)** (versão de referência já gerada, na raiz do repositório) e mostrar o código no editor. Os prompts continuam sendo apresentados a partir deste arquivo. Confira a versão de referência com os critérios do P5.
