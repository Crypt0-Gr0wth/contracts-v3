# Chapitre 2 — Le proxy central ERC1967 et le decoupage en actions

`nProxy.sol` (`contracts/proxy/nProxy.sol`) est un proxy ERC1967 standard (heritage d'OpenZeppelin, `ERC1967Proxy`) qui delegue chaque appel entrant vers une implementation unique. A la difference de l'Euler Vault Kit deja documente ailleurs dans cette bibliotheque, Notional n'utilise pas un routage par module interne : c'est le contrat d'implementation lui-meme (`Router.sol`, non entierement detaille ici) qui contient une fonction `fallback` qui redirige chaque selecteur de fonction vers l'un des contrats d'action deployes separement (`BatchAction`, `AccountAction`, `VaultAction`, `TradingAction`, `nTokenAction`, etc., tous dans `contracts/external/actions/`).

Cette architecture en actions permet de garder le contrat d'implementation principal sous la limite de taille de code de 24 Ko (EIP-170) tout en offrant une API unifiee a l'utilisateur, qui interagit toujours avec la meme adresse de proxy quelle que soit l'action appelee.

`nBeaconProxy.sol` est un second type de proxy, base sur le patron beacon (`contracts/proxy/beacon/`), utilise specifiquement pour les jetons ERC20 wrapper de Notional (pCash, pDebt, nToken, chapitre 6 et 9) : plutot que chaque jeton stocke sa propre adresse d'implementation, tous les proxies beacon d'un meme type pointent vers un beacon commun, ce qui permet de mettre a jour simultanement l'implementation de tous les jetons wrapper d'un coup en changeant seulement l'adresse enregistree dans le beacon.

[Chapitre suivant : Cash Group et Market, les marches de pret a taux fixe](03-cashgroup-market.md)
