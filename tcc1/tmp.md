### 🎯 Sobre o escopo e viabilidade do TCC

1. **Quando você fala em "ambiente controlado", o que exatamente você imagina?** Um escritório? Uma sala de reunião? Uma casa inteligente com sensores? Isso impacta diretamente a fundamentação e o design experimental.
R: Ambiente controlado será definido como um cenário com variáveis parcialmente controladas de ruído, número de participantes e contexto de interação, como:
- sala residencial simulada (ex. sala de estar, quarto)
- escritorio com 2 ou mais pessoas
- sem ruído extremo (ex. rua, transito pesado)
Controle aplicado:
- número limitado de falantes (1–3 pessoas)
- ausência de sobreposição intensa de fala
- ruído de fundo leve/moderado (TV, ventilador, etc.)
A ideia é reduzir complexidade do mundo real, mas ainda mantendo realismo suficiente.

2. **Você pretende trabalhar com áudio real (wav/sinal acústico) ou com texto (transcrições de fala)?** Pergunto porque seus artigos selecionados misturam abordagens:
   - Alguns trabalham no nível acústico (VAD, features MFCC, prosódia)
   - Outros trabalham no nível textual (LLMs, BERT, transcrições ASR)
   - Alguns são multimodais (áudio + texto + vídeo)
   
   Isso muda completamente a complexidade e a viabilidade do TCC.
R: O trabalho focará no nível textual, utilizando transcrições de fala obtidas via ASR, e não no sinal acústico bruto.
Pipeline base: Áudio → ASR → Texto → Limpeza -> NLP ->NLU → Classificador de intenção -> OUTPUT

3. **Você vai construir um dataset do zero (gravar voluntários falando) ou usar datasets públicos existentes?** No objetivo secundário 2 você menciona "construir um dataset", mas isso é muito trabalhoso. Existem datasets como Fluent Speech Commands, Google Speech Commands, etc. Qual sua intenção real?
R: Contruir um dataset do zero, focando exclusivamente em portugues brasileiro, podemos utilizar os datasets como Fluent Speech Commands, Google Speech Commands, etc mas precisariamos traduzir para portugues brasileiro, após ter um dataset base utilizar o classificador de intencao para classificar as intencoes de transcricoes de videos do youtube com o intuito de validar e melhorar o modelo. Como vamos focar no classificador textual, o dataset será composto por transcrições de fala, ou seja, o texto final transcrito.

4. **Qual modelo/abordagem você está inclinado a usar?** Exemplos:
   - Fine-tuning de um modelo pré-treinado (BERT, Whisper)?
   - LSTM/CNN treinado do zero?
   - Abordagem baseada em LLM (como alguns dos seus artigos selecionados)?
R: Quando falamos de modelo temos os modelos de ASR (Automatic Speech Recognition) e os modelos de NLU (Natural Language Understanding). O modelo de ASR será utilizado para transcrever o áudio para texto, e o modelo de NLU será utilizado para classificar a intenção do texto. Podemos utilizar BERTimbau (focado em português) ou modelos similares baseados em Transformers com alternativas de Logistic Regression + TF-IDF, SVM linear, etc.

5. **Você tem acesso a GPU ou pretende treinar na CPU/Colab?** Isso limita quais modelos são viáveis.
R: Tenho disponivel uma GPU RTX A2000 12GB, então posso treinar modelos que requerem GPU. 

---

### 📚 Sobre os artigos selecionados

6. **Na planilha TCC.xlsx existe informação adicional dos artigos antes do afunilamento?** Vi que o CSV tem 15 artigos selecionados. Preciso entender se o .xlsx tem mais contexto sobre critérios de exclusão.
R: Sim, a planilha TCC.xlsx tem informação adicional dos artigos antes do afunilamento. Serao aceitos apenas artigos entre 2021 e 2026, se o artigo for de 2020 ou anterior será desconsiderado, a menos que seja um artigo seminal na área. Eu li o resumo de cada um deles, e selecionei os que mais se aproximam do meu tema, porém meu ingles nao é fluente, então gostaria que você revisasse a seleção e me ajudasse a entender melhor cada artigo. 

7. **Notei que a coluna "Aceito" no CSV está vazia para todos os artigos.** Você já fez alguma seleção final ou todos os 15 estão no jogo?
R: Todos que eu coloquei em selected_articles.csv eu considerei como aceitos, ou seja, são os artigos que eu gostaria de utilizar no meu TCC. Os outros eu considerei como descartados. Mas como mencionei antes, nao tenho certeza absoluta se tomei as melhores decisoes na hora do afunilamento.

8. **Seus artigos selecionados cobrem bem Device-Directed Speech Detection (DDD), mas noto a ausência de artigos seminais/clássicos** como:
   - Lugosch et al. (2019) — "Speech Model Pre-training for End-to-End Spoken Language Understanding" (precursor da classificação de intenção end-to-end)
   - Devlin et al. (2019) — BERT (se for usar abordagem textual)
   - Radford et al. (2023) — Whisper (se for usar ASR)
   
   Isso é proposital? Você pretende citar apenas artigos de pesquisa aplicada, ou quer incluir os fundamentos também?
R: Não foi proposital, eu gostaria de incluir os fundamentos também. Eles sao de suma importância para o meu trabalho.

---

### 🧪 Sobre a hipótese e metodologia

9. **Sua hipótese menciona "características linguísticas e contextuais de curto prazo" — o que você quer dizer com "contextuais de curto prazo"?** É sobre os últimos N segundos de conversa? É sobre o histórico recente de turnos de diálogo?
R: Refere-se a informações linguísticas presentes na própria sentença ou em enunciados imediatamente anteriores, sem considerar histórico longo de conversação.
Exemplo:
"apaga a luz" → depende do contexto recente
mas NÃO usa histórico longo de diálogo

10. **Como você pretende medir "taxas de falsa ativação aceitáveis"?** Qual seria o baseline? Você mencionou comparar com wake-words — tem ideia de quais métricas/thresholds?
R: Serão utilizadas métricas de classificação como: Precision, Accuracy, Recall, F1-score. Foco principal: minimizar falsos positivos (ativação indevida)

11. **Sobre a comparação com wake-words (objetivo secundário 5):** como você faria isso na prática? Implementaria um detector de wake-word simples, ou usaria dados da literatura?
R: A comparação será feita de forma conceitual e indireta, utilizando: dados da literatura sobre precisão de wake-words e análise comparativa de taxas de erro

---

### 📝 Sobre a escrita e entrega

12. **O professor pediu "hipótese de pesquisa" como seção separada?** Vi que você colocou dentro do Capítulo 1 (Introdução). No template do professor, não existe essa seção. Confirma que é requisito?
R: Sim, de forma opcional, a hipótese foi incluída como seção para explicitar claramente a proposição central do trabalho, mesmo não estando explicitamente destacada no template.

13. **Referencial teórico e Fundamentos: qual a diferença que o professor espera?** O template separa os dois. Você tem orientação sobre isso?
R: O referencial teorico deve apresentar os principais conceitos, teorias e definições que fundamentam o trabalho. O referencial teórico deve fornecer ao leitor a base necessária para compreender o problema e a solução proposta. Organize esta seção por temas ou conceitos, não por autor. Cada subseção deve abordar um conceito relevante, explicando-o e relacionando-o ao contexto do trabalho.
Por exemplo: se o trabalho envolve desenvolvimento web, aborde conceitos como arquitetura cliente-servidor, APIs REST, padrões de projeto, etc. Se envolve inteligência artificial, explique os algoritmos e técnicas que serão utilizados.
Utilize citações para fundamentar cada conceito apresentado. Segundo \citeonline{Wazlawick2020}, o referencial teórico deve demonstrar que o autor domina os fundamentos necessários para conduzir a pesquisa.
Agora nos Fundamentos, aprofunde os conceitos técnicos que serão utilizados na solução proposta. Diferentemente do referencial teórico (que apresenta conceitos gerais), os fundamentos devem detalhar as tecnologias, algoritmos, frameworks ou metodologias específicas que serão empregados no desenvolvimento.
Por exemplo:
\begin{itemize}
    \item Se o trabalho utiliza aprendizado de máquina, explique os algoritmos escolhidos (árvores de decisão, redes neurais, SVM, etc.);
    \item Se o trabalho envolve desenvolvimento de software, descreva as tecnologias (linguagens, frameworks, bancos de dados);
    \item Se envolve análise de dados, explique as métricas e técnicas estatísticas que serão aplicadas.
\end{itemize}

Utilize figuras, diagramas e tabelas para ilustrar conceitos quando apropriado.

14. **Qual a data limite dessa entrega parcial?** Isso define quanto preciso priorizar.
R: 3 dias.
-
