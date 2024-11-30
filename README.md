# BASIC PITCH SPOTIFY

## 1. O QUE É A BASIC PITCH?
A Basic Pitch é uma biblioteca python desenvolvida pelo Spotify que tem o intuito de utilizar uma rede neural para  Automatic Music Transcription (AMT).
A biblioteca foi lançada em conjunto com a publicação do Spotify na ICASSP 2022.
O artigo é intitulado (em tradução livre):
"Um Modelo Leve e Agnóstico a Instrumentos para Transcrição de Notas Polifônicas e Estimativa de Múltiplos Tons".
O artigo esclaresse que por instrumentos agnósticos eles querem dizer 'não específico a uma classe de instrumentos'.

---

## 2. O que é AMT e sua Aplicação?
- **Definição**: AMT é o processo de conversão de música (geralmente em áudio) em notação musical, identificando notas, tempos e frequências.
- **Desafios**:
  - Reconhecimento de notas em músicas polifônicas.
  - Processamento eficiente de grandes quantidades de dados.
  - Generalização entre diferentes instrumentos.

---

## 3. Contexto do Modelo NMP
-Criar um modelo leve e agnóstico a instrumentos que seja eficaz em transcrever músicas polifônicas e monofônicas sem re-treinamento, utilizando recursos limitados.

---

## 4. Modelo NMP: Estrutura e Funcionalidade
- **Arquitetura**:
  - Modelo totalmente convolucional.
  - Três saídas de posteriorgrama: 
    1. **Yo**: Início da nota.
    2. **Yn**: Nota ativa.
    3. **Yp**: Tom ativo.
- **Uso de Harmonic Stacking**:
  - **Transformada de Constant-Q (CQT)** aplicada para representar as frequências de forma logarítmica.
  - **Harmonic CQT (HCQT)** alinha frequências harmônicas ao longo de uma terceira dimensão para melhor captação das relações harmônicas.

---

## 5. Processamento e Treinamento do Modelo
- **Entrada**: Áudio de 2 segundos com taxa de amostragem de 22.050 Hz.
- **Função de Perda**:
  - Entropia cruzada binária para cada saída.
  - Perda balanceada para Yo devido ao desbalanceamento de classes.
- **Augmentações de Áudio**: Incluem adição de ruído, filtros de equalização e reverberação.

---

## 6. Experimentos e Resultados
- **Métricas Utilizadas**:
  - **F-measure**: Para medir a precisão das transcrições em notas.
  - **Acurácia de quadro (Acc)**: Percentual de acertos em cada quadro de tempo.
  - **F-no Offset (Fno)**: Considerando apenas o início e a nota ativa, sem a consideração do offset.
- **Desempenho**: 
  - O modelo NMP supera o baseline MI-AMT em várias métricas e em diversos datasets, como MAESTRO, Slakh, e GuitarSet.
  - Performance consistente em dados polifônicos e monofônicos.
  - Comparação com modelos específicos para instrumentos mostra que NMP, apesar de não superar modelos como OF para piano ou Vocano para vocais, se destaca em dados agnósticos a instrumentos como o GuitarSet.

---
        


## 7. Comparações de NMP com Outros Modelos
- **Instrumentos Específicos**: Modelos como **Vocano** (vocal) e **TENT** (guitarra) são especializados para tarefas específicas, enquanto o NMP é agnóstico a instrumentos.
- **Desempenho**:
  - Para guitarras, NMP supera TENT, alcançando resultados de ponta.
  - Para piano e vocais, modelos específicos ainda apresentam melhor desempenho, mas NMP ainda é competitivo.

---

## 8. Múltiplos Tons e Estimativa de Pitches (MPE)
- **MPE**: Estimativa de múltiplos tons em peças polifônicas, utilizando a saída de **Yp**.
- **Resultados**: NMP apresentou melhores resultados no dataset Bach 10, mas ficou atrás do modelo Deep Salience no dataset Su.
- **Importância do Yp**: Embora a resolução de 3 bins por semitom seja baixa, ela ainda é útil para capturar nuances como vibrato e ornamentações.

---

## 9. Eficiência Computacional
- **Benchmarking**:
  - NMP demonstrou ser mais eficiente em termos de uso de memória e tempo de processamento em comparação com o modelo MI-AMT.
  - Para arquivos mais longos, NMP usou apenas 951 MB de memória e 24 segundos, enquanto MI-AMT exigiu 3.3 GB e 96 segundos.
- **Implicações**: Isso mostra que o NMP é uma solução de baixo recurso, adequado para dispositivos com limitações computacionais.

---

## 10. Conclusões
- **Principais Contribuições do NMP**:
  - Modelo eficiente, agnóstico a instrumentos, capaz de lidar com transcrição de notas polifônicas e estimativa de múltiplos tons.
  - Desempenho competitivo com modelos especializados, especialmente em dados mais variados.
  - Maior eficiência computacional, ideal para aplicações em dispositivos com recursos limitados.
  
- **Futuro da Pesquisa**:
  - Melhorias na criação de eventos de nota, com modelos mais refinados.
  - Exploração de compressão e poda de modelos clássicos para reduzir ainda mais os requisitos computacionais.
  - Melhorias na transcrição de misturas de áudio contendo múltiplos instrumentos.

---


