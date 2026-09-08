# Chapitre 11 — BatchAction et les scenarios de liquidation locale et croisee

`BatchAction.sol` permet de regrouper plusieurs operations (deposer, emprunter, preter, fournir de la liquidite, transferer de l'fCash) en une seule transaction, une optimisation de gas essentielle etant donne que chaque operation individuelle sur Notional implique potentiellement une mise a jour de portefeuille et un recalcul de collateral libre.

La liquidation (documentee en detail dans `contracts/internal/liquidation/_README.md`) distingue la devise locale (celle que le liquidateur doit fournir) de la devise de collateral (celle que le compte liquide detient), et definit une invariante stricte : un compte liquide ne peut jamais ressortir de la liquidation avec plus de dette qu'avant, et son collateral libre doit strictement augmenter. Selon la combinaison d'actifs detenus, plusieurs routes de liquidation coexistent — `LiquidateCurrencyAction.sol` pour les liquidations en devise locale ou croisee via cash, nToken ou jeton de liquidite, et `LiquidatefCashAction.sol` specifiquement pour la liquidation d'fCash positif detenu comme collateral.

Le benefice apporte au compte liquide par chaque route est calcule explicitement en formule dans le README (par exemple pour la liquidation de nTokens : `nTokenPresentValue * (liquidationHaircut - haircut)`), une transparence deliberee qui permet a un liquidateur externe de simuler off-chain le montant exact qu'il recevra avant de soumettre sa transaction, plutot que de decouvrir le resultat apres coup.

[Chapitre suivant : le module TradingAction et l'execution directe de trades fCash](12-trading-governance.md)
