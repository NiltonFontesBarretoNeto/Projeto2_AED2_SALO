# Análise Estrutural da Malha Viária de Salo, Finlândia
**Aluno:** Nilton Fontes Barreto Neto 

**Matrícula:** 20250070771

**Disciplina:** DCA3702 – Estrutura de Dados II

**Região de estudo:** Cidade de Salo – Finlândia
  
**Ferramentas:** OSMnx · NetworkX · Gephi 0.11.2

---

## Justificativa da Região de Estudo

**Salo** é uma cidade de porte médio localizada na região de **Finland Proper (Varsinais-Suomi)**, a sudoeste da Finlândia, às margens do rio Uskelanjoki. Conhecida como antiga sede da Nokia, a cidade concentra cerca de 55.000 habitantes e integra os municípios da Grande Área de Turku.

No ano de 2016 realisei um intercâmbio para essa região e achei interessante usá-la como modelo para este projeto, tendo em vista que se trata de uma região consideravelmente pequena e como morei na região por um período de 1 ano possuo certa familiaridade com a região.

Espera-se que a análise revele alta concentração de betweenness nos corredores centrais e nas conexões com a E18, núcleos k-core bem definidos na área central, e closeness elevada nas interseções próximas ao centro comercial e à estação ferroviária.

## Links da plataforma Loom

* **Link referente ao vídeo geral:** [(https://www.loom.com/share/f54ba710b765473199fac0db7188cd95)]

---

## Objetivos da Análise

1. **Hubs de Bairro:** Identificar quais cruzamentos internos (além das grandes avenidas) sustentam a conectividade do bairro.
2. **Caminhos Mínimos:** Analisar como a estrutura viária facilita ou dificulta o acesso aos serviços essenciais dentro de Lagoa Nova.
3. **Decomposição K-Shell:** Localizar o "núcleo duro" do bairro — as ruas que formam a sub-rede mais densamente conectada.
4. **Pontos de Estrangulamento:** Verificar se o tráfego interno de Lagoa Nova possui dependência crítica de poucas vias.

---

## Metodologia e Métricas Calculadas

A análise estrutural da malha viária do bairro de Lagoa Nova foi conduzida seguindo as etapas abaixo:

1. **Obtenção dos Dados (OSMnx):** Download e modelagem da rede viária simplificada direcionada para tráfego terrestre diretamente do OpenStreetMap.
2. **Modelagem Matemática e Processamento (NetworkX):** Construção do grafo e cálculo das métricas de centralidade e conectividade estrutural em ambiente Python.
3. **Visualização Topológica (Gephi):** Exportação da rede para formato `.gexf` e refinamento visual (utilizando o layout ForceAtlas2) para contrastar a estrutura física com a topologia da rede.
4. **Análise Estatística (Seaborn & Pandas):** Geração de histogramas de distribuição, funções acumuladas e correlação cruzada entre as métricas.

### Métricas Estruturais Calculadas:
* **Grau dos Nós ($k$):** Quantidade de conexões diretas de cada interseção viária (grau de entrada/saída simplificado para vias bidirecionais).
* **Distribuição de Grau ($P(k)$ e $P_c(k)$):** Frequência empírica (PDF) e acumulada (CDF) para avaliar a homogeneidade da malha.
* **Centralidade de Intermediação (*Betweenness Centrality*):** Mede a frequência com que um nó atua como ponto de passagem no caminho mais curto entre quaisquer pares de nós.
* **Centralidade de Proximidade (*Closeness Centrality*):** Mede a facilidade de acesso a partir de um determinado cruzamento para todos os outros nós da rede.
* **Centralidade de Autovetor (*Eigenvector Centrality*):** Avalia a importância de um nó com base na centralidade de seus vizinhos imediatos (hubs).
* **Decomposição K-Shell / K-Core:** Particionamento recursivo da rede para identificar o núcleo mais densamente conectado e as franjas periféricas.

---

## Métricas e Visualizações (Escopo Local)

Para o bairro, as figuras agora refletem detalhes mais granulares:

| Ref. | Foco da Análise em Salo | Arquivo |
| --- | --- | --- |
| **Fig 01** | **Malha Viária:** Representação geográfica da rede de vias do bairro. | [fig01_malha_viaria (1).png] |
| **Fig 02** | **PDF e CDF de Grau:** Distribuição empírica de probabilidade do grau dos nós. | [fig02_distribuicao_grau (1).png] |
| **Fig 03** | **Hubs Principais:** Identificação geográfica dos 10 principais cruzamentos/hubs. | [fig03_hubs_map (1).png] |
| **Fig 04** | **Betweenness (Mapa):** Centralidade de intermediação ao longo da malha. | [fig04_betweenness (1).png] |
| **Fig 05** | **Closeness (Mapa):** Centralidade de proximidade (acessibilidade dos nós). | [fig05_closeness (1).png] |
| **Fig 06** | **K-Shell:** Visualização geográfica da decomposição k-shell da rede. | [fig06_kcore_kshell (1).png] |
| **Fig 07** | **Eigenvector (Mapa):** Centralidade de autovetor destacando nós conectados a hubs. | [fig07_eigenvector (1).png] |
| **Fig 08** | **PairGrid de Métricas:** Gráfico de correlação cruzada entre as métricas. | [fig08_pairgrid_metricas (1).png] |
| **Fig 09** | **Matriz de correlação:** Matriz de correlação cruzada entre as métricas. | [fig09_matriz_correlacao (1).png] |

### Visualizações e Layouts no Gephi

Em relação a vizualização dos layouts gerados no **Gephi** foi possível apenas gerar os dados a partir do ForceAtlas2, ocorreu algum erro que não fui capaz de corrigir
na execução do puglin do GeoLayout. Porém os dados gerados na primeira execução do Gephi no puglin mencionado anteriormente estão inclusas nes projeto.

---

## Respostas às Questões 

---
## Questões Analíticas Obrigatórias

1. **Os nós com maior grau coincidem com os nós de maior betweenness?**  
   Não. Nenhum dos nós estão em ambos os rankings. Cruzamentos com grau alto nem sempre são gargalos de fluxo. Pontes e acessos à E18 têm alto betweenness com grau moderado.

2. **O núcleo identificado pelo k-core coincide com os principais hubs?**  
   Não coincide de forma significativa. Apenas 4 dos 20 hubs analisados pertencem ao max-core (k=2). O k-core identifica a área central de Salo, com alta densidade
   de vias internas e redundância de rotas.
3. **O que a métrica de betweenness revela que o grau não revela?**  
   O Betweenness identifica 'pontes' da rede: nós com papel estrutural crítico mesmo com grau baixo. Travessias do rio Uskelanjoki e acessos à E18 são exemplos típicos em Salo.

4. **O que muda entre a visualização geográfica e o layout estrutural?**  
  Não foi possível gerar a visualização geográfica mas o layout estrutural gerado pelo ForceAtlas2 está invertido verticalmente mas pode-se perceber o formato geográfico da cidade bem distribuido.

5. **Existem regiões críticas para mobilidade urbana?**  
   Sim, as travessias do Uskelanjoki e nós de acesso à E18. A remoção desses pontos de alto betweenness fragmentaria a rede, isolando distritos inteiros.

6. **A rede parece homogênea ou apresenta concentração estrutural?**  
  Apresenta concentração estrutural gerada pela fusão de 10 municípios em 2009 criou um núcleo central denso e múltiplas periferias rurais de baixa
   coesão, conectadas por poucos corredores viários. Um exemplo disso pode ser notado quando a região de Halikko (local onde se situa a escola à qual estudei durante o período do intercâmbio) se juntou
   com a região geral de Salo, entre outros municípios que foram unificados à essa regoião.

8. **Os resultados obtidos fazem sentido considerando o conhecimento urbano da região?**  
    Sim. A estrutura encontrada é coerente com a história de Salo: cidade industrial (ex-cede da Nokia) orientada pelo eixo E18 (Helsinque–Turku), com crescimento radial a partir do centro
   histórico e extensas zonas rurais nos limites municipais. Possui um grande fluxo da sua região rodoviária e ferroviária, pois trata-se de uma cidade intermediária de duas cidades bem maiores que ela: Turku
   (Cidade mais portuária e maior zona comercial) e Helsinki (a capital do País).  

---
## Discussão Crítica e Conclusões
A análise da malha viária de Salo mostrou que a cidade possui uma estrutura concentrada em alguns corredores estratégicos, principalmente nos acessos à E18 e nas travessias do rio Uskelanjoki. As métricas de centralidade evidenciaram que nem sempre os cruzamentos com maior número de conexões são os mais importantes para o fluxo urbano, já que vários nós com alto betweenness atuam como pontos críticos mesmo possuindo grau moderado.

A decomposição k-core indicou que a região central possui maior densidade e redundância de rotas, enquanto áreas periféricas dependem de poucos acessos para se conectar ao restante da cidade. Esse comportamento está relacionado ao crescimento histórico de Salo e à fusão dos municípios ocorrida em 2009.

Os resultados obtidos também fazem sentido considerando o contexto urbano da região, influenciado pela antiga presença da Nokia e pela posição estratégica da cidade entre Helsinki e Turku.

Apesar das limitações encontradas no Gephi e da simplificação da rede analisada, o trabalho demonstrou que métricas de teoria dos grafos são ferramentas eficientes para identificar hubs, gargalos estruturais e padrões de conectividade urbana. Dessa forma, conclui-se que a rede viária de Salo possui boa conectividade central, mas apresenta dependência significativa de poucos corredores estratégicos para manter sua integração urbana.


---
