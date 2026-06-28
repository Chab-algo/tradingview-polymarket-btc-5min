# tradingview-polymarket-btc-5min

Indicateur **Pine Script (TradingView)** pour **backtester une stratégie de pari BTC up/down sur 5 minutes**, façon marché binaire **Polymarket**.

## Pourquoi un moteur de backtest custom

Polymarket up/down est un pari **binaire** : on achète une part « Up » (ou « Down ») à un prix `p` compris entre 0 et 1.

- Si on a **raison** → la part vaut 1$ → gain net = `mise × (1/p − 1)`
- Si on a **tort** → la part vaut 0$ → perte = `mise`

Le seuil de rentabilité (breakeven) en taux de réussite est exactement `p`. Le backtester natif de TradingView raisonne en P&L de prix, pas en payout binaire — d'où un moteur de backtest binaire intégré directement dans l'indicateur.

## Fichier

- [`pine/btc-polymarket-5min-backtest.pine`](pine/btc-polymarket-5min-backtest.pine) — indicateur + moteur de backtest.

## Utilisation

1. Ouvrir un graphique **BTC** sur TradingView en unité de temps **5 minutes**.
2. Pine Editor → coller le contenu de `pine/btc-polymarket-5min-backtest.pine` → *Add to chart*.
3. Régler les paramètres dans les réglages de l'indicateur :
   - **Modèle Polymarket** : bankroll initiale, mise par round, prix d'entrée (odds), frais.
   - **Signal de prédiction** : mode (EMA momentum / RSI / suivi de bougie / contre-tendance) et ses paramètres.
4. Lire le tableau de stats en haut à droite : rounds, win rate, breakeven, **edge**, bankroll, P&L, ROI.

> 💡 La stratégie est rentable uniquement si le **win rate > breakeven** (= prix d'entrée). L'**edge** affiché doit être positif.

## Modes de signal

| Mode | Prédiction pour la prochaine bougie |
|------|-------------------------------------|
| EMA momentum | Up si EMA rapide > EMA lente |
| RSI | Up si RSI > seuil |
| Suivi de bougie | Up si la bougie courante est Up (momentum) |
| Contre-tendance | Up si la bougie courante est Down (mean reversion) |

La résolution se fait **sans lookahead** : la prédiction calculée à la bougie `t-1` est confrontée au sens réel de la bougie `t`.

## Workflow

- Chaque modification fait l'objet d'un **commit dédié**, poussé au fur et à mesure.

## À venir

- Nouveaux modes de signal et filtres (volatilité, sessions horaires).
- Gestion de mise variable (Kelly, martingale, etc.).
