# Chapitre 4 — PortfolioHandler : le portefeuille en tableau ou en bitmap

Notional centralise tous les actifs fCash et jetons de liquidite d'un compte dans un unique « portefeuille » pour simplifier le calcul de collateral libre et eviter a l'utilisateur de deplacer des jetons entre contrats. Le depot propose deux implementations distinctes, documentees dans `contracts/internal/portfolio/_README.md`.

Le « portfolio array » (`PortfolioHandler.sol`) n'est pas un tableau Solidity classique — un index de tableau consommerait un slot de stockage complet de 32 octets, beaucoup trop cher. La longueur du tableau est stockee comme un `uint8` dans l'« account context » et sert a calculer les offsets de stockage. Le tableau est trie a chaque chargement (par identifiant de devise, puis echeance, puis type d'actif), jamais stocke trie, ce qui garantit par exemple qu'un jeton de liquidite est toujours immediatement suivi de son fCash correspondant s'il existe.

Le « bitmap portfolio » (`BitmapAssetsHandler.sol`) restreint un compte a ne detenir que de l'fCash dans une seule devise, encode sur 256 bits ou chaque bit signale la presence d'un actif a une echeance donnee, decoupee en quatre blocs temporels de granularite croissante (jours, semaines de 6 jours, mois de 30 jours, trimestres de 90 jours, detailles au chapitre 8 sur le reglement). En echange de cette restriction, un compte bitmap peut detenir beaucoup plus d'actifs dans une seule devise pour un cout en gas bien moindre (~5000 gas par actif) qu'un portefeuille array equivalent.

[Chapitre suivant : le calcul de collateral libre](05-valuation.md)
