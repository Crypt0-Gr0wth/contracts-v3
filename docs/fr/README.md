# Parcours francais de Notional V3 — Pret a taux fixe et variable

Lecture commentee du protocole de pret Notional V3, en francais, un mecanisme par chapitre.
Aucun code n'a ete installe, compile ni execute : ce parcours est purement documentaire.

1. [Presentation de Notional V3](01-presentation.md)
2. [Le proxy central ERC1967 et le decoupage en actions](02-proxy-actions.md)
3. [Cash Group et Market : les marches de pret a taux fixe par fCash](03-cashgroup-market.md)
4. [PortfolioHandler : le portefeuille en tableau ou en bitmap](04-portfolio.md)
5. [Le calcul de collateral libre et les decotes de risque](05-valuation.md)
6. [Prime Cash et Prime Debt : le pret a taux variable introduit par V3](06-prime-cash.md)
7. [InterestRateCurve : le detail du calcul de trade fCash](07-interestratecurve.md)
8. [nToken : la part de liquidite fongible et incitee](08-ntoken.md)
9. [Le reglement trimestriel des marches et de l'fCash idiosyncratique](09-settlement.md)
10. [VaultConfiguration : les coffres a effet de levier avec strategie externe](10-vaults.md)
11. [BatchAction et les scenarios de liquidation locale et croisee](11-batch-liquidation.md)
12. [TradingAction et GovernanceAction : executer des trades et administrer le protocole](12-trading-governance.md)
13. [Limites connues et perimetre de ce parcours](13-limites-et-perimetre.md)
