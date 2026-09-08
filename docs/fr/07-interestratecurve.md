# Chapitre 7 — InterestRateCurve : le detail du calcul de trade fCash

`InterestRateCurve.sol` (656 lignes, le plus long fichier du module markets) contient l'implementation exacte de `calculatefCashTrade`, la fonction appelee par `Market.executeTrade` (chapitre 3) a chaque emprunt, pret ou fourniture de liquidite qui modifie la composition d'un marche.

La fonction retourne trois valeurs : le montant net de prime cash echange (`netPrimeCash`), la part de ce montant qui revient a la reserve du protocole (`netPrimeCashToReserve`, via `RESERVE_FEE_SHARE`), et le taux d'interet implique apres application des frais (`postFeeInterestRate`). Un trade dont le `netPrimeCash` retourne est zero est considere comme ayant echoue silencieusement — `Market.executeTrade` ne met a jour l'etat du marche que si cette valeur est non nulle, evitant d'ecrire en stockage pour un trade qui n'a en realite rien echange.

Chaque trade reussi declenche un evenement `Emitter.emitfCashMarketTrade` qui journalise le compte, la devise, l'echeance et les montants echanges — ces evenements servent de source de verite hors-chaine pour reconstituer l'historique des taux d'un marche sans avoir a interroger le stockage a chaque bloc historique.

[Chapitre suivant : nToken, la part de liquidite fongible et incitee](08-ntoken.md)
