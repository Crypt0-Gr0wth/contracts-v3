# Chapitre 12 — TradingAction et GovernanceAction : executer des trades et administrer le protocole

`TradingAction.sol` (417 lignes) est le point d'entree externe pour executer un trade fCash directement contre un marche donne, sans passer par les actions de plus haut niveau comme `AccountAction` (pret/emprunt simple) — utile notamment pour les coffres a effet de levier (chapitre 10) qui ont besoin d'un controle fin sur le type de trade execute (`TradeActionType`, un enum couvrant l'achat/vente d'fCash, l'ajout/retrait de liquidite et le reglement de portefeuille).

`GovernanceAction.sol` centralise les fonctions reservees a la gouvernance du protocole : listage de nouvelles devises, mise a jour des parametres de cash group et de vault, et gestion de la reserve du protocole (`TreasuryAction.sol`). Le README principal du depot precise que la gouvernance de Notional est actuellement detenue par un multisig Gnosis 3-sur-5, dont deux signataires sont les fondateurs du protocole et trois sont des membres de la communaute — un modele de decentralisation graduelle justifie par la complexite du systeme et la necessite de pouvoir reagir rapidement en cas d'incident, en particulier autour des evenements periodiques comme l'initialisation trimestrielle des marches.

`ActionGuards.sol` fournit les modificateurs communs reutilises par la plupart des actions externes pour verifier que l'appelant a l'autorisation requise et que le protocole n'est pas en pause, evitant de dupliquer cette logique dans chaque contrat d'action.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
