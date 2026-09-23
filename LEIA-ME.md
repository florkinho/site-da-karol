# Nosso cantinho — Yudi & Karol

## Atualizar o site existente

O site continua estático. Copie os arquivos da pasta `site` do pacote para a raiz do repositório `site-da-karol`, mantendo a pasta `assets` junto dos HTMLs. Faça uma cópia da versão antiga antes de substituir. Não é necessário instalar um banco de dados ou configurar chaves.

As páginas são `index.html`, `fazenda.html`, `investigacao.html`, `rpg.html` e `quebracabeca.html`. Os dois últimos jogos e as fotos foram preservados da versão original. Os estilos e scripts novos também precisam ser enviados; não copie apenas os HTMLs.

## Progresso

A fazenda e a campanha de investigação salvam no navegador e no endereço em que vocês jogam. Fechar a página não para as plantações. Apagar os dados do navegador apaga esse progresso. Um endereço de prévia e o endereço do GitHub têm saves separados. Para manter o progresso dos jogos antigos e do Tony, atualize o mesmo endereço que vocês já usam.

Na fazenda, escolham Yudi ou Karol no topo para deixar e receber bilhetes. Esse nome identifica o jogador da vez; não é uma conta ou senha. Os sons só tocam quando ativados, e o botão permite silenciar novamente. Comecem colhendo os dois canteiros dourados, depois plantem morangos e visitem os bichinhos.

## Novos casos

As três histórias estão em `case-data.js`, separadas do motor do jogo. Para acrescentar um caso, adicione um objeto ao array `CASES` com um `id` novo e permanente, `number`, `title`, `place`, `date`, `tag`, `color`, `summary`, `intro`, `brief`, `suspects`, `evidence`, `puzzles`, `deductions` e `solution`.

O número de enigmas e deduções é variável e a interface acompanha as quantidades do caso. O quarto caso está em case-advanced.js, carregado depois de case-data.js. Tipos de enigma: `code`, `choice`, `grid` e `order`. As habilidades são `logic`, `perception` e `empathy`. `needs` aponta para documentos que precisam ser examinados; `requires` em um documento aponta para o enigma que o libera. Não crie dependências circulares. IDs de documentos e enigmas são internos a cada caso.

As deduções contêm `id`, `a`, `b`, `relation` (`contradiz` ou `explica`) e `text`. A solução contém o `suspect`, o `motive` exato, a lista `motives`, o ID da `proof` decisiva e o encerramento `ending`. Não altere IDs de casos já lançados: isso preserva os avanços de vocês. As soluções ficam nos arquivos, como em qualquer jogo estático; não abram o código do caso antes de jogar se quiserem evitar spoilers.

## Desenvolvimento

Sem dependências. `node build.cjs` valida os scripts e links internos e copia os arquivos públicos para `dist`. O código-fonte continua nos HTMLs, CSSs e scripts da raiz.

Sons e respectivas licenças estão em `creditos.html`. A música original da página inicial usa o player externo que já existia e precisa de internet. As fontes externas têm alternativas locais.

## Guia da investigação (sem revelar soluções)

Os três casos iniciais são: O relógio que parou; O cofre de vidro; A última flor da estufa. Cada pasta contém nove documentos, quatro suspeitos, três enigmas e duas deduções.

- **Ocorrência:** contexto da história e perguntas que a dupla precisa responder.
- **Documentos:** examinar uma prova registra a leitura. Envelopes fechados são liberados ao solucionar o enigma indicado.
- **Depoimentos:** perguntas e respostas dos quatro suspeitos. Comparem com os documentos; o jeito de falar, sozinho, não prova culpa.
- **Enigmas:** códigos, horários, ordenação de eventos, cifra/Morse, mapas e proporções, conforme o caso. Leiam os documentos indicados antes de responder. Errar permite tentar de novo.
- **À frente agora:** escolhe qual investigador empresta sua habilidade à próxima rolagem. Os dois recebem XP mesmo quando apenas um conduz.
- **Dados:** uma rolagem de D6 por enigma. Dado + habilidade do personagem >= 5 revela a primeira pista gratuitamente. A falha não bloqueia o desafio. O resultado é salvo, e trocar o investigador não permite rolar outra vez.
- **Consultar pista:** mostra ajuda sem depender de sorte. Cada consulta reduz em 5 XP a recompensa futura daquele enigma, até o mínimo de 10 XP por pessoa. Não retira XP já ganho. O foco começa em 3 por caso e diminui ao consultar pistas; chegar a zero não impede novas consultas.
- **Quadro de pistas:** relaciona duas provas examinadas usando Contradiz ou Explica. É preciso encontrar as duas deduções previstas pelo caso. Não é um quadro que interpreta qualquer frase livre.
- **Caderno:** espaço livre para hipóteses. As anotações são salvas quando vocês saem do campo.
- **Relatório:** fica disponível após todos os enigmas e deduções do caso. Escolham responsável, motivo e prova decisiva. Uma conclusão incorreta mantém o caso aberto. Acertar mostra a reconstituição e dá 60 XP a cada um.
- **Fichas da dupla:** mostram XP, nível e habilidades. Cada 100 XP acumulados aumentam o nível e dão um ponto para distribuir. Cada habilidade chega a +5. Yudi começa com Lógica +2, Percepção +1 e Escuta +0; Karol, com Lógica +0, Percepção +1 e Escuta +2. As habilidades dão bônus no dado do enigma correspondente; não respondem o enigma automaticamente.
- **Evolução:** um enigma dá 20 XP por pessoa antes do desconto das pistas. Um caso inicial completo sem pistas manuais dá 120 XP para cada um. Rever um caso encerrado não repete as recompensas. As fichas continuam entre casos.
- **Salvamento:** a campanha fica neste navegador e aparelho. Não sincroniza entre celulares. Voltar ao arquivo não apaga o caso; use Continuar caso para retomar.

Ordem sugerida: Ocorrência → Documentos e Depoimentos → Enigmas → novos Documentos → Quadro de pistas → Relatório.


## Desenho às cegas

A página desenho-as-cegas.html está ligada ao início e à aba Brincar. O catálogo blind-characters.js tem 23 grupos com cinco personagens cada: os 22 desenhos pedidos e Mickey e sua turma como bônus. A rodada sorteia quem descreve, quem desenha e um personagem dos grupos selecionados. O nome só aparece para quem descreve, antes de passar o aparelho. Depois de esconder o nome, quem desenha inicia os 90 segundos. O tempo continua com a aba em segundo plano; depois dele, o desenho é bloqueado e surge o campo do palpite. O resultado aceita acentos e apelidos cadastrados, com tolerância de uma letra para nomes com cinco ou mais letras. Novas rodadas evitam repetir personagens até esgotar as opções selecionadas. A rodada atual é guardada temporariamente na aba do navegador, inclusive desenho e horário de término. Fechar a aba pode descartar esse registro temporário.

Referências de nomes: https://irmaodojorel.com.br/ ; https://www.nickanimation.com/content/the-fairly-odd-parents/ ; https://www.paramountplus.com/shows/peppa-pig/news/1010752/meet-the-characters-from-peppa-pig/ . Os personagens e séries pertencem aos respectivos titulares. O jogo usa nomes como desafios de desenho, sem imagens oficiais.

## Expansão: teatro e norte

Caso 05 — O aplauso que ninguém ouviu: 13 documentos, quatro suspeitos, oito enigmas e quatro deduções. O arquivo case-theatre.js é carregado após os casos anteriores. Os IDs e saves antigos permanecem.

Ato III — A Torre das Promessas: continua pelo botão no final do Ato II, inclusive em campanhas já salvas. Inclui 25 cenas, duas rotas, dois enigmas digitados, encontros com Oriel e Sarça e um guardião que pode ser convencido ou enfrentado. O cenário das Montanhas do Norte é original. Recompensa única: terceira relíquia e +4 HP máximo para cada herói.


## Caso perito — O arquivo da maré morta

Caso 06, em case-tide.js: 22 documentos, 12 enigmas e 6 deduções. Três frentes encadeadas (expedição, manutenção e autoria), transposição com colunas incompletas, quadrado de coordenadas, rota com limite de exposição, coincidência de ciclos, correção de bits, lógica de gavetas, verificador de lotes, equações de mistura, álibis, cronologia e identidade de amostras. Recompensa máxima: 300 XP por investigador. Pistas opcionais com método, sem necessidade de pesquisa externa.

O jardim de lembranças e seu jogo de pares foram retirados a pedido.
