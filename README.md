# MVP de Machine Learning - Predição de Resultados em Rodadas de CS:GO

Este projeto faz parte de um **MVP de Machine Learning**, cujo objetivo foi **prever o vencedor de rodadas no CS:GO** (Counter-Strike: Global Offensive) com base em dados de telemetria e variáveis contextuais.  

---

##  Objetivo
- Desenvolver um pipeline de Machine Learning para classificar o vencedor da rodada (**Counter-Terrorists - CT** ou **Terrorists - T**).
- Explorar técnicas de **pré-processamento**, **feature engineering** e **modelagem supervisionada**.
- Avaliar os resultados com e sem variáveis derivadas, discutindo trade-offs e limitações.

---

##  Dataset
O dataset contém informações de rodadas de CS:GO, incluindo:
- Economia dos times (ex.: `ct_money`, `t_money`).
- Estado dos jogadores (ex.: `ct_health`, `t_health`, `ct_players_alive`, `t_players_alive`).
- Utilização de granadas (`smoke`, `flashbang`, `molotov`).
- Situação da bomba (`bomb_planted`).
- Contexto temporal (`time_left`).
- **Variáveis criadas via Feature Engineering**, como:
  - `dinheiro_por_jogador_ct` e `dinheiro_por_jogador_t`.
  - `granadas_por_jogador_ct` e `granadas_por_jogador_t`.
  - `eco_balance` (diferença de economia entre CT e T).
  - `tempo_categoria` (Início, Meio, Fim do round).
  - `plantado_com_vivos` (bomba plantada ponderada por jogadores vivos).

---

##  Metodologia
1. **Pré-processamento**  
   - Padronização de variáveis numéricas com `StandardScaler`.  
   - Codificação de variáveis categóricas com `OneHotEncoder`.  
   - Transformação de variáveis booleanas em inteiros.  

2. **Feature Engineering**  
   - Criação de novas variáveis derivadas da economia, granadas e tempo.  
   - Inclusão de interações específicas como `plantado_com_vivos`.  

3. **Modelagem**  
   - Algoritmo principal: **Random Forest Classifier**, otimizado via **RandomizedSearchCV**.  
   - Comparação do modelo com e sem feature engineering.  

4. **Avaliação**  
   - Métricas utilizadas: **Accuracy**, **Precision**, **Recall** e **F1-score**.  
   - Interpretação do modelo via **Feature Importance**.  

---

##  Resultados

### Sem Feature Engineering
- **Accuracy**: ~0.83  
- Principais variáveis: `time_left`, `ct_money`, `t_money`, `bomb_planted`, `ct_health`, `t_health`.  

### Com Feature Engineering
- **Accuracy**: 0.814  
- Principais variáveis após novas features:
  - **Originais dominando**: `t_armor`, `ct_armor`, `t_helmets`, `ct_money`, `t_money`.  
  - **Novas relevantes**: `eco_balance`, `dinheiro_por_jogador_ct`, `dinheiro_por_jogador_t`, `plantado_com_vivos`.  

> Observação: Apesar das novas variáveis trazerem insights, o desempenho global **não superou o modelo base**. Isso mostra que **feature engineering deve ser feito de forma incremental e validado cuidadosamente** — criar muitas variáveis ao mesmo tempo pode introduzir ruído em vez de ganho.

---

##  Conclusões
- O modelo capturou bem aspectos centrais do jogo:
  - **Tempo restante** e **situação da bomba**.  
  - **Economia dos times**.  
  - **Recursos de jogadores (vida, granadas, armaduras)**.  
- A adição de variáveis derivadas trouxe **novas perspectivas interpretativas**, mas não aumentou a acurácia.  
- Sugere-se:
  - Testar **uma variável de cada vez**, validando seu impacto isoladamente.  
  - Explorar algoritmos mais complexos ou ensembles.  
  - Avaliar redução de dimensionalidade para evitar sobrecarga de variáveis derivadas.  

---

##  Próximos Passos
- Implementar novos modelos (ex.: Gradient Boosting, XGBoost, LightGBM).  
- Usar técnicas de **validação cruzada** mais robustas.  
- Avaliar outras abordagens de **feature selection**.  
- Explorar explicabilidade com métodos como **SHAP** (caso haja recursos computacionais).  

---
##  Autor
- **Pedro Dias**  
Projeto desenvolvido como MVP de Machine Learning (2025).
