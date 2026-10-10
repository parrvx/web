### Fase 1: Fundação Analítica e Ingestão de Dados (Semanas 1 a 4)

**Objetivo:** Dominar consultas analíticas de alta performance, manipulação colunar e extração de dados brutos (extratos bancários, PDFs de autos e balancetes) com integridade forense.

#### SQL Analítico & OLAP com DuckDB

* **O que estudar:** [Window functions](https://duckdb.org/docs/2.0/sql/functions/window_functions) ([`OVER`](https://duckdb.org/docs/2.0/sql/functions/window_functions#syntax), [`PARTITION BY`](https://duckdb.org/docs/2.0/sql/functions/window_functions#partition-and-ordering), [`LEAD`](), `LAG`), self-joins, CTEs recursivas, agregação temporal por janelas deslizantes (`time_bucket`), ingestão direta de arquivos sem banco tradicional.
* **Material & Cursos:**
* [Documentação Oficial do DuckDB](): Tutoriais de SQL analítico e extensões de Parquet/JSON.
* Livro: *SQL for Data Analysis: Advanced Techniques for Transforming Data into Insights* (Cathy Tanimura).
* Curso Interativo: *Select Star SQL* (selectstarsql.com) para consolidar consultas complexas.

#### Engenharia de Dados com Polars & Arrow

* **O que estudar:** LazyFrame vs. DataFrame, expressões vetoriais (`pl.col`), junções assíncronas (*asof join* para pareamento temporal de transações), parsing de datas/timestamps e tratamento de dados faltantes.
* **Material:**
* *The Polars User Guide* (guia oficial): Seções de expressões, paralelismo e streaming.
* Livro: *Polars Cookbook* (Damian Farrell).

#### Parsing Forense de Documentos Jurídicos e Bancários

* **O que estudar:**
* Leitura e extração de tabelas em relatórios periciais e autos processuais em PDF via `pymupdf` (FitZ).
* Parser de arquivos bancários padronizados `.ofx` (usando a biblioteca `ofxparse` em Python).
* Algoritmos de hash criptográfico (`hashlib.sha256`) para atestar a cadeia de custódia na ingestão do arquivo.

* **Projeto Prático da Fase 1:** Construir um script que recebe uma pasta com 50 extratos bancários em PDF/OFX de bancos diferentes, extrai as tabelas de lançamentos, gera o hash SHA-256 de cada arquivo e consolida tudo em uma única tabela DuckDB/Parquet indexada por data e titular.

### Fase 2: Matemática Financeira Pericial e Estatística Forense (Semanas 5 a 8)

**Objetivo:** Reconstituir saldos, identificar fraudes contábeis, calcular juros/correções monetárias sem erros de arredondamento e aplicar testes de conformidade matemática.

#### Matemática Financeira Pericial

* **O que estudar:**
* Regimes de juros simples vs. compostos; taxas nominais, efetivas e equivalentes.
* Sistemas de amortização: Tabela Price vs. SAC; cálculo e expurgo pericial de anatocismo (cobrança ilegal de juros sobre juros).
* Reajustes monetários legais por séries temporais do Banco Central (IPCA-E, INPC, CDI, Taxa SELIC acumulada) aplicados vetorizadamente no Polars.

* **Material & Livros:**
* Livro: *Matemática Financeira e suas Aplicações* (Alexandre Assaf Neto).
* Livro: *Perícia Contábil e Financeira* (Valder Luiz Palombo).
* Dados da API SGS do Banco Central do Brasil (pacote Python `python-bcb` para puxar índices oficiais via código).

#### Estatística Forense & Detecção de Fraude

* **O que estudar:**
* **Lei de Benford**: Distribuição do primeiro e segundo dígitos para detectar manipulação humana de valores contábeis e notas fiscais frias.
* **Detecção de Anomalias**: Métricas de dispersão robustas (IQR, Modified Z-score) para flagrar depósitos discrepantes do perfil financeiro.
* **Padrões de Fracionamento (*Smurfing*)**: Algoritmos para detectar múltiplos depósitos logo abaixo de limites de notificação ao COAF (ex: depósitos sucessivos de R$ 9.800,00 ou R$ 49.500,00 em janelas de 48h).

* **Material & Livros:**
* Livro: *Forensic Analytics: Methods and Techniques for Forensic Accounting Investigations* (Mark J. Nigrini) — *A leitura mais essencial de toda a trilha sobre auditoria matemática com dados reais.*

* **Projeto Prático da Fase 2:** Implementar um módulo em Python que recebe uma base de 10.000 lançamentos de despesas de um órgão público/empresa, executa o teste da Lei de Benford, aponta desvios estatísticos com gráficos de conformidade e recalcula a dívida com expurgo de anatocismo aplicando a Taxa SELIC oficial do BACEN.

### Fase 3: Ciência de Redes e Rastreamento ("Follow the Money") com `igraph` (Semanas 9 a 13)

**Objetivo:** Modelar fluxos de capitais ilícitos como redes orientadas e ponderadas, isolar operadores financeiros, detectar consórcios de fachada e exportar layouts limpos.

#### Teoria de Grafos e Análise de Redes Complexas

* **O que estudar:**
* Grafos direcionados (*Directed Acyclic Graphs* - DAGs) e com pesos (*weighted*).
* Algoritmos de caminho mínimo ponderado (*Dijkstra*), fluxo máximo e corte mínimo (*Ford-Fulkerson / Min-cut*).
* Centralidades estruturais: *Betweenness Centrality* (intermediação), *In/Out Degree* (fontes vs. sumidouros), *PageRank*.
* Detecção de comunidades em redes complexas: Algoritmos *Leiden* e *Louvain*.

* **Material & Livros:**
* Livro Aberto: *Network Science* (Albert-László Barabási) — Disponível gratuitamente em *networksciencebook.com*. Capítulos 2, 3 e 9.
* Livro: *Networks: An Introduction* (Mark Newman).
* Documentação Oficial: *python-igraph documentation and tutorial* (`igraph.org/python`).

#### Tipologias de Lavagem de Dinheiro & Investigação Financeira

* **O que estudar:**
* Padrões da ENCCLA e do COAF: mescla de capitais lícitos com ilícitos, triangulação com offshores e operadores (*doleiros*).
* Detecção topológica de **transações em carrossel** (ciclos e loops onde o dinheiro gira entre contas conexas para simular volume ou faturamento fictício).
* Algoritmos de agrupamento para identificar o "Grupo Econômico de Fato" (fusão de nós com base em sócios comuns ou endereços coincidentes).

* **Material de Leitura:**
* Cartilhas Oficiais de Tipologias do COAF (Conselho de Controle de Atividades Financeiras) e GAFI/FATF.
* Framework *Follow The Money* do OCCRP (Organized Crime and Corruption Reporting Project) — documentação do projeto aberto *followthemoney.tech*.

* **Projeto Prático da Fase 3:** Construir uma rotina que recebe transações entre 500 contas correntes, detecta ciclos de transferências fechados (ex: A $\to$ B $\to$ C $\to$ A), calcula o *betweenness centrality* para elencar os 5 maiores operadores de repasse e projeta as coordenadas 2D do fluxo hierárquico com o algoritmo de Sugiyama via `igraph`.

### Fase 4: O Laudo Pericial, Prova Jurídica e Automação com Typst (Semanas 14 a 16)

**Objetivo:** Transformar as evidências técnicas computacionais em laudos periciais judiciais aceitos em tribunal, estruturados formalmente e reprodutíveis via código.

#### Direito Processual Pericial e Normas Técnicas

* **O que estudar:**
* **CPC/2015**: Arts. 464 a 479 (Prova Pericial), requisitos do perito judicial, dever de imparcialidade, resposta formal a quesitos do juiz e das partes, e quesitos suplementares.
* **Normas Brasileiras de Contabilidade**:
* **NBC TP 01 (R1)**: Perícia Contábil (planejamento, execução, termos de diligência, estrutura do laudo).
* **NBC PP 01 (R1)**: Do Perito (competência técnico-profissional e impedimentos legais).

* **Material:**
* Código de Processo Civil comentado (Capítulo de Provas).
* Texto integral das normas NBC TP 01 e PP 01 publicadas pelo CFC (Conselho Federal de Contabilidade).

#### Tipografia Forense e Automação Documental com Typst

* **O que estudar:**
* Estruturação de documentos técnicos com numeração sequencial de parágrafos periciais.
* Ingestão nativa de dados tabulares (`csv(...)`, `json(...)`) sem necessidade de copiar/colar planilhas manualmente.
* Inclusão de diagramas vetoriais SVG gerados pelo `igraph` com diagramação precisa em grade milimétrica.
* Manutenção do ambiente selado com `flake.nix` para garantir que o parecer possa ser compilado idêntico daqui a 10 anos.

* **Material:**
* Documentação Oficial do Typst (`typst.app/docs`).

* **Projeto Final Integrador:** Simulação completa de uma Perícia Judicial de Fraude Financeira:
1. Leitura de base de extratos brutos com geração de tabela de hash SHA-256 da cadeia de custódia.
2. Filtragem de dados atípicos e transações fracionadas com DuckDB e Polars.
3. Cálculo e expurgo de anatocismo/juros ilegais com aplicação de séries temporais do BACEN.
4. Mapeamento da rede com `igraph` isolando as contas operadoras via *betweenness* e gerando o SVG do fluxo hierárquico.
5. Compilação automática do Laudo Pericial completo em PDF via Typst, contendo: folha de rosto processual, síntese metodológica, respostas item por item aos quesitos do juízo, tabela dinâmica das contas e diagrama do caminho do dinheiro.

### Resumo Cronológico de Leituras Obrigatórias

1. **Básico / Dados:** *SQL for Data Analysis* (Cathy Tanimura) + Documentação do Polars.
2. **Matemática & Auditoria:** *Forensic Analytics* (Mark J. Nigrini) + *Matemática Financeira e suas Aplicações* (Assaf Neto).
3. **Redes & Vínculos:** *Network Science* (Barabási) + Documentação do `python-igraph`.
4. **Normativo:** CPC/2015 (arts. 464–479) e Norma NBC TP 01 do CFC.

