# Chapitre 1 — Presentation de Notional V3

Notional est un protocole de pret a taux fixe fonde sur le concept d'fCash : un jeton representant une creance ou une dette a une echeance et un montant fixes, negocie sur des marches a courbe de liquidite internes (chapitre 3). La version V3 de ce depot ajoute au-dessus du pret a taux fixe existant un systeme de pret a taux variable appele « prime cash » et « prime debt » (chapitre 6), qui elimine plusieurs frictions historiques de V2 autour du reglement des positions a l'echeance.

Le protocole tourne autour d'un unique contrat proxy central (le « Notional proxy ») qui route les appels vers des contrats d'action externes (`contracts/external/actions/`), tandis que la logique metier reutilisable vit dans des bibliotheques internes (`contracts/internal/`). Chaque devise geree par Notional (ETH, DAI, USDC...) a son propre « cash group » (chapitre 4) qui definit un ensemble de marches a differentes echeances, et peut optionnellement avoir un ou plusieurs « leveraged vaults » (chapitre 10) permettant d'emprunter avec effet de levier pour des strategies specifiques.

Ce parcours s'appuie sur le depot clone a la date d'ecriture, branche `master-v3`. Fichiers centraux : `contracts/internal/markets/Market.sol`, `contracts/internal/markets/CashGroup.sol`, `contracts/internal/markets/InterestRateCurve.sol`, `contracts/internal/portfolio/` (PortfolioHandler, BitmapAssetsHandler), `contracts/internal/vaults/` (VaultConfiguration, VaultAccount), `contracts/external/actions/` et `contracts/external/proxies/PrimeCashProxy.sol`.

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : le proxy central et le decoupage en actions](02-proxy-actions.md)
