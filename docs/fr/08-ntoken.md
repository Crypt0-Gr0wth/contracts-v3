# Chapitre 8 — nToken : la part de liquidite fongible et incitee

Fournir de la liquidite directement a un marche (chapitre 3) donne des jetons de liquidite specifiques a une echeance, peu pratiques a echanger. Notional propose donc le nToken (`nTokenAction.sol`, `nTokenMintAction.sol`, `nTokenRedeemAction.sol`, tous dans `contracts/external/actions/`) : un jeton fongible par devise qui represente une part proportionnelle de liquidite repartie automatiquement sur l'ensemble des marches actifs de cette devise, plus les incitations associees.

`nTokenAction.sol` (331 lignes) expose les fonctions de vue permettant de calculer la valeur presente d'un nToken (`nTokenPresentValue`) ainsi que sa valeur apres decote de risque (`nTokenHaircutValue = nTokenPV * haircut`), une distinction cruciale reutilisee telle quelle dans le module de liquidation (chapitre 11) ou les nTokens peuvent etre achetes a une decote de liquidation plus genereuse que leur decote de risque normale.

Les nTokens sont incites automatiquement (`Incentives.sol`, module balances) : chaque changement de solde nToken d'un compte declenche la reclamation automatique des incitations accumulees, evitant a l'utilisateur une transaction separee. Le README du module balances precise egalement que les nTokens sont toujours strictement one-to-one avec un jeton negociable sur Notional, ce qui permet de stocker leur solde dans le meme slot de stockage que le solde de jeton sous-jacent et d'economiser un acces au stockage.

[Chapitre suivant : le reglement trimestriel des marches et de l'fCash](09-settlement.md)
