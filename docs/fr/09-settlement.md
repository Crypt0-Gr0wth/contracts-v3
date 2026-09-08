# Chapitre 9 — Le reglement trimestriel des marches et de l'fCash idiosyncratique

Le reglement (`contracts/internal/settlement/_README.md`) est declenche automatiquement lorsqu'un compte transige et que son `nextSettleTime` indique que des actifs ont depasse leur echeance. L'fCash, denomine en montant sous-jacent fixe, se regle en prime cash au « settlement rate » de sa devise et de son echeance — un taux unique fige la premiere fois qu'un fCash de cette echeance se regle, garantissant que tout l'fCash de la meme echeance et devise se convertit au meme taux, ce qui preserve l'invariant que la somme algebrique du prime cash cree par le reglement est toujours nulle.

Les jetons de liquidite se reglent differemment : toujours tous les trimestres (jamais a leur echeance propre), independamment de la date de maturite de leur marche. Un jeton de liquidite se regle en une reclamation de cash fixe et une position fCash residuelle, qui peut ne pas arriver a echeance en meme temps que le reglement du jeton de liquidite lui-meme — ce residu porte le nom d'« ifCash » (fCash idiosyncratique) et reste dans le portefeuille du fournisseur de liquidite jusqu'a sa propre echeance ou jusqu'a ce qu'il soit echange.

Pour les portefeuilles bitmap (chapitre 4), le reglement implique une manipulation bit a bit specifique documentee en detail dans le README du module : au fil du temps, des echeances doivent migrer d'un bloc temporel a granularite grossiere (par exemple mensuel) vers un bloc plus fin (journalier), un processus de « remapping » de bits qui utilise les proprietes arithmetiques des diviseurs communs entre blocs (1, 6, 30, 90 jours).

[Chapitre suivant : VaultConfiguration, les coffres a effet de levier](10-vaults.md)
