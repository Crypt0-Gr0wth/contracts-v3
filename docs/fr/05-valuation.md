# Chapitre 5 — Le calcul de collateral libre et les decotes de risque

Le module de valorisation determine, pour chaque compte, si sa position nette (`netPortfolioValue + netCashBalance + netNTokenValue`, convertie en une devise de reference via les taux de change) reste positive apres application de decotes de risque (« haircuts ») sur chaque type d'actif detenu en collateral.

Chaque cash group definit plusieurs parametres de risque stockes en `uint8` pour l'efficacite en gas et remis a l'echelle a l'usage : `FCASH_HAIRCUT` (decote appliquee a l'fCash positif detenu en collateral), `DEBT_BUFFER` (marge de securite ajoutee au cote dette), `LIQUIDITY_TOKEN_HAIRCUT` (decote sur les jetons de liquidite, qui representent une position mixte cash/fCash) et `RATE_ORACLE_TIME_WINDOW` (fenetre de lissage temporel du taux utilise pour la valorisation, distincte du taux instantane utilise pour l'execution des trades).

Un compte devient eligible a la liquidation (chapitre 11) uniquement lorsque son collateral libre passe negatif, ce qui ne peut arriver que s'il detient un solde de cash ou d'fCash negatif quelque part dans son portefeuille. Le systeme distingue explicitement le taux « oracle » utilise pour la valorisation (lisse dans le temps pour resister a la manipulation instantanee) du taux utilise pour executer un trade reel sur un marche, une separation deliberee documentee dans `Market.sol` : la version view (`buildAssetRateView`) ne doit jamais servir a calculer un trade reel.

[Chapitre suivant : Prime Cash et Prime Debt, le pret a taux variable](06-prime-cash.md)
