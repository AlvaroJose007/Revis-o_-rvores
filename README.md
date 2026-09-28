# Revisao_arvores

Nome: Álvaro José Marinho Pinho
Disciplina: Estrutura de Dados II 
Professora: Profa. Kadidja Valéria 
Modalidade: Individual, remota e assíncrona 
Conceitos Fundamentais de Árvores
Antes de analisar cada estrutura, importa recapitular as definições estruturais base: 
•	Nó: Unidade elementar de armazenamento que guarda uma chave/dado e ponteiros/referências para outros nós. 
•	Raiz: O nó de topo da hierarquia, o único nó da árvore que não possui pai. 
•	Pai e Filho: Numa relação direta de descendência, o nó de nível superior imediato é o pai; os nós diretamente acessíveis a partir dele são os seus filhos. 
•	Folha: Qualquer nó que não possua nós-filhos (grau zero). 
•	Altura: Comprimento do caminho mais longo da raiz até à folha mais profunda (medido pelo número de arestas ou nós). 
•	Percurso: Ordem sistemática de visitação de todos os nós (pré-ordem, em-ordem, pós-ordem ou em largura/nível). 
Etapa 1 — Revisão Bibliográfica
1. Árvore Geral
•	Organização dos dados: Hierarquia genérica onde cada nó pode possuir um número arbitrário de filhos (grau irrestrito).
•	Propriedade a manter: Ausência de ciclos e existência de um único caminho entre a raiz e qualquer outro nó.
•	Busca e inserção: A busca requer percursos exaustivos (busca em profundidade/DFS ou largura/BFS), com complexidade $O(n)$ no pior caso. A inserção requer a indicação do nó pai onde o novo nó será anexado.
•	Ajustes: Não há balanceamento automático intrínseco.
•	Contexto de uso: Modelação de hierarquias reais, como sistemas de ficheiros (pastas e subpastas), organigramas organizacionais e representação de documentos DOM/XML/JSON.
2. Árvore Binária (Geral)
•	Organização dos dados: Cada nó possui, no máximo, dois nós-filhos, convencionalmente denominados filho esquerdo e filho direito.
•	Propriedade a manter: Grau máximo por nó igual a 2.
•	Busca e inserção: Sem ordenação semântica prévia, a busca é $O(n)$. A inserção é realizada na primeira posição livre disponível.
•	Ajustes: Não possui mecanismos intrínsecos de balanceamento.
•	Contexto de uso: Árvores de decisão de escolha binária, árvores de expressões aritméticas e base estrutural para especializações ordenadas.
3. Árvore Binária de Busca (ABB / BST)
•	Organização dos dados: Estrutura binária ordenada.
•	Propriedade a manter: Para qualquer nó $x$, todas as chaves na sua subárvore esquerda são estritamente menores que a chave de $x$, e todas as chaves na sua subárvore direita são maiores (ou iguais, consoante a convenção).
•	Busca e inserção: A busca compara a chave pretendida com o nó atual e desce para a esquerda ou para a direita, alcançando custo médio $O(\log n)$. A inserção segue o caminho de busca e cria a nova folha no ponto terminal.
•	Ajustes: Não possui balanceamento dinâmico. Inserções ordenadas podem degenerar a estrutura numa lista linear, degradando operações para $O(n)$.
•	Contexto de uso: Dicionários e coleções dinâmicas em memória onde as inserções ocorrem de forma aleatória ou a simplicidade de implementação é prioritária.
4. Árvore AVL
•	Organização dos dados: Árvore binária de busca estritamente auto-balanceada.
•	Propriedade a manter: Para cada nó, o fator de balanceamento $FB = \text{altura}(\text{subárvore esquerda}) - \text{altura}(\text{subárvore direita})$ deve pertencer obrigatoriamente ao conjunto $\{-1, 0, +1\}$.
•	Busca e inserção: Busca em tempo garantido $O(\log n)$. A inserção realiza o processo da ABB, seguido pela atualização das alturas e verificação do $FB$ no caminho de regresso até à raiz.
•	Ajustes: Havendo desbalanceamento ($\vert{}FB\vert{} > 1$), aplicam-se rotações simples (à esquerda ou à direita) ou duplas (esquerda-direita ou direita-esquerda).
•	Contexto de uso: Aplicações intensivas em consultas e leitura rápida, onde as operações de inserção/remoção são menos frequentes do que as leituras.
5. Árvore Rubro-Negra (Red-Black Tree)
•	Organização dos dados: Árvore binária de busca com balanceamento aproximado baseado em coloração de nós (cada nó é Vermelho ou Preto).
•	Propriedades a manter:
1.	Todo o nó é vermelho ou preto.
2.	A raiz é sempre preta.
3.	Folhas nulas (nós sentinela NIL) são pretas.
4.	Um nó vermelho não pode ter filhos vermelhos (não há nós vermelhos consecutivos).
5.	Todos os caminhos simples de um nó até às folhas descendentes contêm o mesmo número de nós pretos (black-height).
•	Busca e inserção: Busca em $O(\log n)$. A inserção insere o nó com cor vermelha e corrige eventuais violações da propriedade 4.
•	Ajustes: Recolorações e, quando necessário, rotações (no máximo duas rotações por inserção).
•	Contexto de uso: Estruturas de dados de bibliotecas padrão de linguagens de programação (ex.: std::map/std::set em C++, TreeMap em Java) e escalonadores de processos em sistemas operativos (ex.: Completely Fair Scheduler do Linux).
6. Árvore B
•	Organização dos dados: Árvore de busca balanceada multipaginada (multiway), com nós capazes de armazenar múltiplas chaves e ponteiros.
•	Propriedade a manter: Numa árvore de ordem $m$, cada nó (exceto a raiz) possui pelo menos $\lceil m/2 \rceil - 1$ chaves e no máximo $m - 1$ chaves. Todas as folhas encontram-se rigorosamente no mesmo nível de profundidade.
•	Busca e inserção: A busca realiza uma pesquisa interna (frequentemente binária) dentro de cada nó/página carregada e ramifica para o apontador adequado. A inserção insere a chave na folha apropriada em ordem.
•	Ajustes: Se um nó exceder a capacidade máxima, ocorre uma cisão (split): a chave mediana é promovida para o nó pai e o nó divide-se em dois.
•	Contexto de uso: Sistemas de gestão de bases de dados (SGBDs) e sistemas de ficheiros que operam em memória secundária (discos magnéticos e SSDs), reduzindo drasticamente o número de acessos de E/S (I/O).
7. Árvore B+
•	Organização dos dados: Especialização da Árvore B onde apenas as folhas guardam dados/registos efetivos. Os nós internos funcionam exclusivamente como índice/guia. Adicionalmente, todas as folhas encontram-se ligadas sequencialmente entre si por uma lista duplamente/simplesmente ligada.
•	Propriedade a manter: Chaves dos nós internos são replicadas nas folhas. Todas as folhas estão no mesmo nível e ligadas horizontalmente.
•	Busca e inserção: Toda a busca pontual desce obrigatoriamente até ao nível folha. A inserção acomoda a chave na folha e pode propagar cópias de chaves para os níveis superiores em caso de split.
•	Ajustes: Cisões de nós e redistribuição de chaves similares à Árvore B.
•	Contexto de uso: Padrão de facto para índices primários e secundários em bancos de dados relacionais modernos (ex.: motor InnoDB do MySQL, PostgreSQL) devido ao excelente desempenho em consultas por intervalo (range queries).
8. Heap (Binário)
•	Organização dos dados: Árvore binária completa (ou quase completa preenchida da esquerda para a direita), habitualmente serializada diretamente num vetor linear.
•	Propriedade a manter: Em Max-Heap, o valor de cada nó é maior ou igual aos valores dos seus filhos (o elemento máximo está sempre na raiz). Em Min-Heap, o inverso.
•	Busca e inserção: A inserção coloca o elemento no fim do vetor e executa a subida (heapify-up ou sift-up), custando $O(\log n)$. A remoção do elemento de topo substitui a raiz pelo último elemento e executa a descida (heapify-down ou sift-down).
•	Ajustes: Trocas sucessivas de posição entre pai e filho para restabelecer a ordem da heap.
•	Contexto de uso: Filas de prioridade, algoritmo de ordenação Heapsort e algoritmo de caminho mínimo de Dijkstra.
9. Trie (Árvore de Prefixos)
•	Organização dos dados: Árvore de pesquisa n-ária onde as arestas ou nós representam símbolos/caracteres individuais. As palavras são representadas pelos caminhos percorridos a partir da raiz.
•	Propriedade a manter: Nós que partilham o mesmo prefixo partilham a mesma cadeia de ancestrais.
•	Busca e inserção: O tempo de busca depende exclusivamente do comprimento da chave de busca $k$, custando $O(k)$, independentemente da quantidade total de elementos $n$.
•	Ajustes: Criação de novos ramos a partir da primeira letra divergente; não requer rotações.
•	Contexto de uso: Sistemas de autocompletar em caixas de pesquisa, corretores ortográficos, tabelas de roteamento IP e índices de genoma/bioinformática.
Etapa 2 — Quadro Comparativo
Estrutura PNG	Organização dos dados PNG	Regra ou propriedade PNG	Operação ou ajuste PNG	Aplicação PNG	Referência PNG
Árvore Geral	Hierarquia genérica de nós com grau arbitrário.	Ausência de circuitos fechados; raiz única e caminho único até cada nó.	Percursos estruturais (DFS/BFS); anexação em nó pai específico.	Estruturas de pastas/diretórios de ficheiros; árvores sintáticas (AST).	Cormen et al. (2012)
Árvore Binária	Cada nó possui no máximo 2 filhos (esquerdo e direito).	Grau $\le 2$ para todos os nós.	Inserção em primeiro nó disponível; percursos pré/em/pós-ordem.	Árvores de decisão binárias; representação de expressões aritméticas.	Szwarcfiter & Markenzon (2010)
ABB	Nós binários com critério posicional ordenado. 	Subárvore esquerda $<$ nó atual $<$ subárvore direita. 	Descida orientada por comparação; sem rotações automáticas (pode degenerar). 	Tabelas de símbolos e dicionários básicos em memória. 	Sedgewick & Wayne (2011) 
AVL	ABB com controlo estrito de alturas. 	Fator de balanceamento $FB \in \{-1, 0, +1\}$ em todos os nós. 	Rotações simples (E, D) ou duplas (ED, DE) após inserção/remoção. 	Dicionários em memória com foco primordial em leitura rápida. 	Szwarcfiter & Markenzon (2010) 
Rubro-negra	ABB com coloração de nós (vermelho/preto). 	Raiz preta; sem nós vermelhos consecutivos; igual número de nós pretos até às folhas. 	Recoloração de nós e rotações simples/duplas (máx. 2 rotações na inserção). 	std::map/std::set (C++ STL), TreeMap (Java), CFS (Kernel Linux). 	Cormen et al. (2012) 
B	Nós multipaginados contendo múltiplas chaves e apontadores. 	Todas as folhas no mesmo nível; nós com ocupação entre $\lceil m/2 \rceil - 1$ e $m - 1$ chaves. 	Cisão (split) com promoção da mediana ou fusão (merge) de nós. 	Índices de ficheiros em disco e motores clássicos de bases de dados. 	Elmasri & Navathe (2011) 
B+	Nós internos atuam só como índices; folhas contêm dados e apontador horizontal. 	Chaves internas repetidas nas folhas; folhas encadeadas sequencialmente ao mesmo nível. 	Cisões propagadas para cima; percurso sequencial facilitado entre folhas. 	Índices B-Tree de SGBDs modernos (MySQL/InnoDB, PostgreSQL). 	Silberschatz et al. (2020) 
Heap (Binário)	Árvore binária completa mapeada sequencialmente num vetor.	Propriedade de Max-Heap (pai $\ge$ filhos) ou Min-Heap (pai $\le$ filhos).	Subida (heapify-up) na inserção; descida (heapify-down) na extração da raiz.	Filas de prioridade, Heapsort, Algoritmo de Dijkstra.	Cormen et al. (2012)
Trie	Árvore de caracteres/símbolos associados a arestas/nós.	Chaves com mesmo prefixo partilham o mesmo trajeto a partir da raiz.	Inserção letra a letra criando nós para novos carateres; busca sem colisões.	Mecanismos de autocompletar, dicionários T9, tabelas de encaminhamento IP.	Sedgewick & Wayne (2011)
Etapa 3 — Identificação por Analogias
1. Uma estante de números é reorganizada por rotações quando um lado fica alto demais em relação ao outro.
•	Estrutura identificada: Árvore AVL. 
•	Justificativa técnica: A AVL baseia-se no cálculo sistemático da diferença de altura entre as subárvores esquerda e direita (fator de balanceamento). Quando essa diferença ultrapassa 1 em módulo, são disparadas operações de rotação (à esquerda, à direita, dupla à esquerda ou dupla à direita) para restabelecer o equilíbrio estrito. 
•	Limite da analogia: Na vida real, reorganizar uma prateleira ou estante física implica deslocar fisicamente livros/objetos ao longo de um mesmo plano de suporte; numa árvore AVL, as rotações alteram ponteiros lógicos entre pai e filhos sem deslocação física de espaço, modificando a topologia hierárquica sem comprometer a ordem de busca in-order.
2. Um catálogo guarda várias chaves por página; quando uma página fica cheia, ela é dividida.
•	Estrutura identificada: Árvore B. 
•	Justificativa técnica: Cada nó da Árvore B comporta um conjunto ordenado de chaves (semelhante a uma página de catálogo). Quando um nó atinge o limite máximo de chaves ($m-1$), ocorre a operação de cisão (split), em que a chave mediana é promovida para o nó ascendente e o restante é particionado em duas novas páginas irmãs. 
•	Limite da analogia: Um catálogo em papel divide-se criando uma nova folha contígua física; na Árvore B, o particionamento pode provocar um efeito em cascata de promoções até à raiz, fazendo a árvore crescer para cima (aumentando a sua altura global), o que não tem correspondência direta num catálogo estático encadernado.
3. Uma fila mantém a tarefa de maior prioridade no topo para retirá-la primeiro.
•	Estrutura identificada: Heap (Max-Heap) / Fila de Prioridade. 
•	Justificativa técnica: Na Max-Heap, a raiz da árvore contém obrigatoriamente a maior chave da coleção (propriedade de ordem da heap), garantindo acesso ao elemento prioritário em tempo constante $O(1)$ e extração com reorganização em $O(\log n)$.
•	Limite da analogia: Uma fila comum sugere uma estrutura puramente sequencial (FIFO - first-in, first-out); a Heap é uma árvore binária quase completa onde os nós fora do topo não estão ordenados sequencialmente entre si, mantendo apenas relações de dominância vertical pai-filho.
4. Um índice percorre letras sucessivas e compartilha o início das palavras de mesmo prefixo.
•	Estrutura identificada: Trie (Árvore de Prefixos). 
•	Justificativa técnica: A Trie estrutura os dados de modo a que cada aresta ou nó represente um único caractere. Termos com prefixos comuns partilham integralmente a mesma sequência de nós até ao caractere onde se diferenciam. 
•	Limite da analogia: Num índice alfabético tradicional de um livro, as palavras completas estão listadas por extenso; na Trie, a palavra não existe armazenada como uma cadeia única e estática num único nó, mas sim como a rota percorrida desde a raiz até uma marcação de fim de palavra.
5. Uma estrutura usa cores, recolorações e rotações para manter controlada a altura dos caminhos de busca.
•	Estrutura identificada: Árvore Rubro-Negra (Red-Black Tree). 
•	Justificativa técnica: A Árvore Rubro-Negra utiliza um bit extra por nó para codificar a sua cor (vermelho ou preto) e faz cumprir regras específicas de balanceamento. Quando ocorre uma inserção, ela prioriza recolorações de nós para restabelecer as propriedades e recorre a rotações apenas quando a recoloração não basta. 
•	Limite da analogia: No mundo físico, alterar a cor de um objeto é uma propriedade puramente estética sem impacto estrutural; na árvore rubro-negra, a cor é um invariante matemático rigoroso que garante formalmente que nenhum caminho seja mais do que duas vezes maior do que qualquer outro.
6. Um índice conduz às folhas que contêm os registros, ligadas entre si para facilitar consultas por intervalo.
•	Estrutura identificada: Árvore B+. 
•	Justificativa técnica: Na Árvore B+, os nós intermediários servem unicamente como guia de navegação, enquanto todos os registos de dados reais residem exclusivamente no nível das folhas. As folhas são interligadas através de ponteiros horizontais sequenciais (lista duplamente ligada), viabilizando varrimentos por intervalo (range scans) sem necessidade de retroceder aos níveis superiores da árvore. 
•	Limite da analogia: Uma analogia de índice convencional sugere um índice no fim de um livro onde cada entrada remete para uma página diferente do volume; na Árvore B+, as próprias folhas contêm o corpo dos registos (ou o agrupamento principal do ficheiro) e fornecem a navegação horizontal contínua de forma independente da hierarquia superior.
7. Numa coleção de números, cada nó direciona valores menores para a esquerda e maiores para a direita.
•	Estrutura identificada: Árvore Binária de Busca (ABB / BST). 
•	Justificativa técnica: Trata-se da regra de ordenação canónica da ABB: para cada nó com chave $K$, qualquer valor da sua subárvore esquerda satisfaz $\text{chave} < K$ e qualquer valor da sua subárvore direita satisfaz $\text{chave} > K$. 
•	Limite da analogia: A analogia sugere uma bifurcação física estática com capacidade ilimitada e perfeita distribuição; no entanto, uma ABB sem mecanismo de reequilíbrio pode tornar-se totalmente desbalanceada se os valores forem inseridos de forma pré-ordenada, perdendo a sua eficiência logarítmica e passando a comportar-se como uma lista linear simplesmente encadeada.
Referências Consultadas
•	CORMEN, Thomas H. et al. Algoritmos: teoria e prática. 3. ed. Rio de Janeiro: Elsevier, 2012.
•	ELMASRI, Ramez; NAVATHE, Shamkant B. Sistemas de Banco de Dados. 6. ed. São Paulo: Pearson, 2011.
•	SEDGEWICK, Robert; WAYNE, Kevin. Algorithms. 4. ed. Upper Saddle River: Addison-Wesley, 2011.
•	SILBERSCHATZ, Abraham; KORTH, Henry F.; SUDARSHAN, S. Sistema de Banco de Dados. 7. ed. Rio de Janeiro: GEN LTC, 2020.
•	SZWARCFITER, Jayme Luiz; MARKENZON, Lilian. Estruturas de Dados e seus Algoritmos. 3. ed. Rio de Janeiro: LTC, 2010.
