# Chapitre 13 — Limites connues et perimetre de ce parcours

Le code de Notional V3 est publie sous licence Business Source License 1.1 (`LICENSE`), qui n'est pas une licence open source permissive au sens strict tant que sa date de conversion (definie par MariaDB Corporation, editeur original de la BSL) n'est pas atteinte — a verifier directement dans le fichier `LICENSE` du depot avant tout usage en production.

Ce parcours ne couvre pas en detail `contracts/internal/balances/Incentives.sol` (mecanique precise de calcul des recompenses), `contracts/bots/` (bots operationnels hors chaine ou contrats d'assistance), `contracts/mocks/` (contrats de simulation utilises par les tests), le detail complet de `contracts/internal/vaults/VaultSecondaryBorrow.sol` (emprunt secondaire multi-devises dans un coffre) ni les adaptateurs de gouvernance externes (`contracts/external/governance/`, `contracts/external/patchfix/`).

Rien n'a ete installe, compile, deploye ni execute pour ecrire ces chapitres. Aucun test n'a ete lance ; ces chapitres decrivent ce que le code Solidity dit faire, en renvoyant aux fichiers cites. Le depot fournit sa propre suite de tests Foundry et Brownie (dossiers `test/` et `tests/`, script `bin/runTests.sh`) pour verification independante.
