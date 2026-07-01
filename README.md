# tradingview-polymarket-btc-5min

Indicateur **Pine Script (TradingView)**, purement **visuel**, pour le marché **Polymarket « Bitcoin Up or Down » sur 5 minutes**.

## Idée

Sur un graphique **BTC en M1**, on regarde la **première bougie d'une minute** de chaque fenêtre M5 (celle qui ouvre à :00, :05, :10, :15…) :

- 1ère bougie **bullish** (clôture > ouverture) → **BUY** (parier *Up*)
- 1ère bougie **bearish** (clôture < ouverture) → **SELL** (parier *Down*)

Puis, au bout des 5 minutes, la fenêtre est **résolue** (clôture de la fenêtre vs son ouverture). Le **fond de la fenêtre** se colorie alors selon le résultat du pari :

- **Vert** si le pari a gagné (résolu dans le bon sens du BUY/SELL)
- **Rouge** si le pari a perdu

Ce n'est **pas** une stratégie et il ne backteste rien : c'est un indicateur visuel.

## Fichier

- [`pine/polymarket-btc-m5-first-minute.pine`](pine/polymarket-btc-m5-first-minute.pine)

## Utilisation

1. Ouvrir un graphique **BTC** en **M1** sur TradingView.
2. Pine Editor → coller le contenu du fichier → *Add to chart*.
3. Régler les options visuelles si besoin (couleurs, fond, labels, séparateur).

## Visuels

- **Fond de la fenêtre M5** coloré selon le **résultat** : vert = pari gagné, rouge = pari perdu.
- **1ère bougie colorée** selon le **signal** (vert = BUY, rouge = SELL).
- **Label BUY / SELL** sur la 1ère bougie.
- **Séparateur vertical** au début de chaque fenêtre M5.
- **Alertes** BUY / SELL (déclenchées à la clôture de la 1ère minute).

> Le signal se confirme à la **clôture de la 1ère minute** : il reste alors 4 minutes pour placer le pari sur Polymarket.
>
> Le fond « résultat » est **rétrospectif** : une fenêtre se colorie quand la suivante démarre (son issue n'est connue qu'à la fin des 5 minutes). Conçu pour BTC 24/7 (5 bougies M1 par fenêtre M5).

## Workflow

- Chaque modification fait l'objet d'un **commit dédié**, poussé au fur et à mesure.
