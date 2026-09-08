# Chapitre 6 — Prime Cash et Prime Debt : le pret a taux variable introduit par V3

L'ajout principal de la V3 par rapport a V2 est un systeme de cash a taux variable appele « prime cash » (creance) et « prime debt » (dette), expose a l'utilisateur sous forme de jetons ERC4626-like via des proxies beacon (chapitre 2) : `PrimeCashProxy.sol` et `PrimeDebtProxy.sol` (`contracts/external/proxies/`).

`PrimeCashProxy` illustre une particularite du systeme : contrairement a un coffre ERC4626 classique ou les actifs sont detenus par le contrat du jeton, ce proxy delegue integralement le solde, l'offre totale et les transferts au contrat Notional central via `NOTIONAL.getBalanceOfPrimeCash`, `NOTIONAL.getPrimeFactors` et `NOTIONAL.pCashTransfer` — le proxy n'est qu'une facade ERC20/ERC4626 pour un solde qui vit entierement dans le stockage du proxy central. Le commentaire du code le note explicitement : « pCash is a non-standard ERC4626 in the sense that assets are held on the proxy and may be liquidated if there is a debt balance as well ».

Le passage a un taux variable pour le reglement des positions fixes change fondamentalement la mecanique de maturite par rapport a V2 : en V3, une position fCash a taux fixe se regle desormais vers le taux variable courant plutot que vers une exigence de reglement cash discrete et figee, ce qui reduit le risque autour des echeances et ameliore les rendements retournes aux fournisseurs de liquidite nToken (chapitre 9).

[Chapitre suivant : InterestRateCurve, le detail du calcul de trade](07-interestratecurve.md)
