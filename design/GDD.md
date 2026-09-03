# Pokémon War of Legends
### Documento de Design (v0.1 — rascunho inicial)

> Este documento é o ponto de partida. Está estruturado para você editar, cortar e expandir — não é uma versão final. Seções marcadas com **[ABERTO]** são decisões que ainda precisam da sua palavra final.

---

## 1. Conceito em uma frase

Um ROM hack completo para GBA (base **pokeemerald-expansion**), com três regiões conectadas por uma guerra ancestral entre forças lendárias, Mega Evolução, Elite Fours múltiplas e uma Pokédex que reúne lendários de todas as gerações.

Referência direta de tom e escopo: **Pokémon Light Platinum** (Fire Red hack, 8 regiões costuradas, dificuldade alta, muito conteúdo pós-jogo) — mas construído sobre uma base de código mais moderna e sustentável para um desenvolvedor solo.

---

## 2. Base técnica

- **Motor:** [pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion) (fork comunitário do pokeemerald com Mega Evolução, split físico/especial, Pokémon até gerações recentes, formas regionais, habilidades modernas, etc. já implementados).
- **Mapas:** Porymap (editor visual, sem necessidade de C).
- **Scripts de eventos/NPCs/diálogos:** Poryscript (linguagem de alto nível que compila para o formato de script do jogo — muito mais legível que script bytecode puro).
- **Toolchain de compilação:** devkitARM + make (ambiente padrão do projeto, com instruções oficiais de build).
- **Sprites/tiles:** Pokémon novos (gerações que a expansão já suporta) entram como assets prontos da comunidade; sprites originais (se quisermos algo 100% autoral depois) via Aseprite/GraphicsGale.
- **Controle de versão:** Git, desde o primeiro commit do fork da engine — essencial para não perder trabalho e poder reverter experimentos.

**Por que essa base e não hackear uma ROM pronta (Fire Red/Emerald) na unha:** Mega Evolução, mais de 4 gerações de Pokémon e múltiplas regiões exigiriam ASM manual extenso do zero no método clássico. Na expansion, esses sistemas já existem — o trabalho fica concentrado em *conteúdo* (mapas, história, times, balanceamento), que é onde o tempo de um dev solo rende mais.

---

## 3. Lore central — "A Guerra dos Lendários"

Milênios atrás, três forças lendárias entraram em conflito pelo destino do mundo:

- **Ordem** — regida por Xerneas, associada à vida, estrutura e permanência.
- **Caos** — regida por Yveltal, associada à destruição, mudança e renovação forçada.
- **Equilíbrio** — regido por Zygarde, que interveio para conter as outras duas forças e selar o conflito antes que o mundo fosse destruído.

O selo de Zygarde dividiu o poder da guerra em fragmentos e os espalhou pelo mundo, escondidos em templos, ruínas e sob a guarda de outros lendários que hoje conhecemos como "guardiões" — cada um retendo uma lasca daquele poder antigo. É por isso que lendários de todas as eras existem nesse mundo: todos são, em alguma medida, ecos daquela guerra original.

**Gancho da trama atual:** uma organização chamada **Equipe Ruína** descobriu fragmentos do selo e acredita que o mundo precisa ser "reiniciado" pela guerra novamente para eliminar a estagnação e a corrupção das sociedades atuais. Eles caçam os guardiões região por região, forçando o jogador — que começa como um treinador comum — a se tornar a pessoa que entende a ligação entre todos esses eventos antes que a Equipe Ruína reative o conflito.

Essa estrutura permite literalmente **todos os lendários no jogo**: cada um é reenquadrado narrativamente como guardião de um fragmento, sem exigir Pokémon fictícios novos (fakemon) — usamos o dex oficial completo.

---

## 4. Mundo — três regiões

| Região | Tema | Papel na história | Nº de Ginásios |
|---|---|---|---|
| **Terravia** | Rural/clássica — florestas, campos, primeira grande cidade | Região inicial. O jogador começa a jornada normal; primeiros indícios da guerra antiga aparecem em ruínas secundárias | 8 |
| **Umbrisk** | Industrial/urbana, com uma cadeia vulcânica ao norte | QG principal da Equipe Ruína; região de meio-jogo, tom mais sombrio | 8 |
| **Aetheris** | Ilhas flutuantes/celeste, pouco povoada, ancestral | Região final — templo original do selo de Zygarde, clímax da história | 6 |

As três regiões são conectadas por rotas de barco/voo desbloqueadas na progressão da história (mesmo padrão de "regiões costuradas" do Light Platinum, mas com transições justificadas na trama em vez de coladas sem explicação).

**[ABERTO]** Nomes de cidades, mapas detalhados e geografia interna de cada região — a fazer numa passada seguinte, depois que a estrutura macro estiver aprovada.

---

## 5. Protagonista, rival e professor

- **Protagonista:** customizável (menino/menina), silencioso, treinador iniciante de Terravia. **[ABERTO]** nome padrão.
- **Rival:** cresce junto com o protagonista, mas se envolve cedo com a Equipe Ruína (não como vilão puro — acredita genuinamente na causa deles) até um arco de redenção em Aetheris. Dá mais peso emocional ao "vilão" do que uma equipe genérica.
- **Professor(a):** especialista em lendários/mitologia regional (não só distribuição de Pokédex) — plot device natural para explicar a lore conforme o jogo avança.

**Iniciais (starters):** Gen 4 — **Turtwig / Chimchar / Piplup**. Escolha deliberada: geração "do meio", pouco repetida em hacks (a maioria usa Kanto/Hoenn), com boa variedade visual e de tipo.

---

## 6. Equipe vilã — Equipe Ruína

- **Motivação:** acreditam que sociedades estagnaram e que só um "reinício" no estilo da guerra antiga pode gerar progresso real. Não são cartunescos — têm um argumento coerente, o que humaniza o conflito.
- **Estrutura:** célula em cada região, com um Admin regional; líder final revelado apenas em Aetheris.
- **Uso de lendários:** cada arco regional termina com a Equipe Ruína tentando capturar/controlar o guardião daquela região — é o que força o jogador a intervir.

---

## 7. Ginásios, Elite Fours e Campeões

Cada região tem sua própria **Elite Four + Campeão** — três "campeonatos" completos ao longo da campanha, não só um no final:

1. **Elite Four de Terravia** (fim do arco 1) — tipos clássicos, dificuldade introdutória.
2. **Elite Four de Umbrisk** (fim do arco 2) — dificuldade intermediária, times temáticos ligados à Equipe Ruína.
3. **Elite Four de Aetheris** (fim do arco 3) — dificuldade alta, campeões usam Mega Evolução.

**Pós-jogo:** **Liga das Três Regiões** — um torneio final que reúne os três Campeões anteriores + o jogador, coroando um "Grande Campeão" — conteúdo pós-game natural, no espírito dos hacks tipo Light Platinum que têm bastante conteúdo depois dos créditos.

**[ABERTO]** Tipos/temas de cada líder de ginásio e membro de Elite Four — próxima passada de design.

---

## 8. Mega Evolução

- Ativada via **Mega Stone + Key Stone** (mesmo sistema oficial), introduzida no meio do arco de Terravia através de uma ruína ligada à guerra antiga.
- **Megas oficiais:** disponíveis progressivamente (ex: Charizard, Gengar, Garchomp, Lucario, etc.), obtidas como recompensa de eventos de história ou side quests com lendários.
- **Megas exclusivas (fan megas) para os iniciais:** Mega Torterra, Mega Infernape, Mega Empoleon — criadas especificamente para esta ROM, já que os iniciais de Gen 4 não têm mega oficial. Reforça a identidade própria do hack.
- Uso por líderes de ginásio/Elite Four introduzido a partir de Umbrisk em diante, para escalar dificuldade.

**[ABERTO]** Lista final de quais espécies recebem Mega Evolução (oficiais incluídas + quantas fan megas além dos iniciais).

---

## 9. Lendários — distribuição (visão geral)

Trio central da trama (ver seção 3): **Xerneas, Yveltal, Zygarde** — arco principal, aparecem em Terravia, Umbrisk e Aetheris respectivamente conforme a história avança.

Demais lendários/míticos, distribuídos como guardiões regionais (capturáveis em ruínas, sidequests e pós-jogo):

| Região | Lendários propostos |
|---|---|
| **Terravia** | Trio de pássaros de Kanto, Mewtwo, Mew, Raikou/Entei/Suicune, Lugia/Ho-Oh, Regis (Regirock/Regice/Registeel/Regigigas) |
| **Umbrisk** | Trio de Hoenn (Groudon/Kyogre/Rayquaza), Deoxys, Dialga/Palkia/Giratina, Heatran, Darkrai, Cresselia |
| **Aetheris** | Trio dos Lagos (Uxie/Mesprit/Azelf), Reshiram/Zekrom/Kyurem, Trio de Unova (Cobalion/Terrakion/Virizion/Keldeo), Tornadus/Thundurus/Landorus, Xerneas/Yveltal/Zygarde (arco principal), Tapus, Solgaleo/Lunala/Necrozma, Zacian/Zamazenta/Eternatus, lendários de Paldea |

Isso cobre a Pokédex Nacional completa de lendários/míticos conhecidos até a geração 9. Alguns entram só no pós-jogo (Liga das Três Regiões desbloqueia acesso de volta a áreas antigas com lendários adicionais, como é comum em hacks grandes).

**[ABERTO]** Distribuição fina — qual lendário fica em qual cidade/ruína específica, e quais exigem sidequest vs. captura direta.

---

## 10. Pokédex

- **Dex Nacional completa** disponível (a expansion já suporta os sprites/dados de todas as gerações).
- Cada região tem sua **Dex Regional** própria (conjunto de ~120–150 espécies "nativas" daquela região, no espírito das dex regionais oficiais), pensada para dar variedade de tipo aos primeiros ginásios sem sobrecarregar o jogador com escolha demais logo de cara.
- Evoluções que dependem de troca/itens especiais mantidas, com ajustes de acessibilidade (ex: evolução por troca também disponível por item, prática comum em hacks solo-friendly).

---

## 11. Roadmap de desenvolvimento (fases)

A ideia é **não tentar construir as três regiões de uma vez** — isso é o que mais historicamente destrói projetos de ROM hack solo.

1. **Fase 0 — Toolchain:** fork do pokeemerald-expansion, ambiente de build funcionando, primeira compilação rodando num emulador sem nenhuma alteração.
2. **Fase 1 — Vertical slice:** uma cidade inicial + rota 1 + primeiro ginásio de Terravia, iniciais funcionando, sistema de Mega Evolução testado com 1 espécie. Objetivo: provar que todo o pipeline (mapa → script → batalha → mega) funciona de ponta a ponta.
3. **Fase 2 — Terravia completa:** os 8 ginásios, Elite Four de Terravia, arco de história local, primeiro guardião lendário.
4. **Fase 3 — Umbrisk completa:** mesmo padrão, incluindo QG da Equipe Ruína.
5. **Fase 4 — Aetheris + clímax:** região final, revelação do trio central, Elite Four final.
6. **Fase 5 — Pós-jogo:** Liga das Três Regiões, lendários adicionais, conteúdo extra.
7. **Fase 6 — Polimento:** balanceamento, playtesting, correções de bugs, tradução/texto final.

**Recomendação:** tratar a Fase 1 como o próximo passo imediato assim que este documento estiver aprovado — é o teste real de "isso é viável no tempo que eu tenho".

---

## 12. Decisões em aberto (resumo)

- [ ] Nomes de cidades e geografia detalhada das 3 regiões
- [ ] Nome padrão do protagonista/rival
- [ ] Tipos e times de cada líder de ginásio e Elite Four (24 líderes + 12 Elite Four + 3 campeões no total)
- [ ] Lista final de espécies com Mega Evolução
- [ ] Colocação exata de cada lendário no mapa
- [ ] Dex regional detalhada (espécie por espécie) de cada região
- [ ] Nome/identidade visual da Equipe Ruína (uniformes, logo, líder final)

---

*Próximo passo sugerido: aprovar/ajustar este documento e depois decidir se entramos na Fase 0 (montar o toolchain) ou continuamos detalhando o design (mapas de Terravia, líderes de ginásio, etc.).*
