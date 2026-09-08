# Chapitre 13 — Limites connues et perimetre de ce parcours

Ce depot melange plusieurs generations de code Solidity (`0.4.24`, `0.8.9`, `0.8.25`) accumulees au fil des mises a niveau successives du protocole depuis son lancement. Cette heterogeneite reflete l'histoire reelle du protocole plutot qu'un choix architectural unique, et complique la lecture pour qui cherche un style de code homogene.

Le dossier `contracts/0.8.25/vaults/` contient une architecture de « coffres de staking » plus recente et plus experimentale, qui etend le modele au-dela du simple pool stETH ; ce parcours ne le couvre pas, le coeur du protocole (Lido, stETH, StakingRouter, file de retraits, oracle) suffisant deja a une lecture complete du mecanisme de liquid staking.

La securite du protocole repose sur plusieurs lignes de defense independantes : le quorum du consensus d'oracle, les `sanity checks` d'`Accounting.sol`, et en dernier ressort la gouvernance de la DAO Lido, qui peut ajuster les roles, les modules et les parametres. Aucune de ces lignes n'est infaillible individuellement ; c'est leur superposition qui constitue la garantie.

Ce parcours ne couvre ni la gouvernance Aragon historique (les votes de la DAO Lido eux-memes), ni les oracles off-chain qui calculent les rapports avant soumission (leur code vit dans un depot separe), ni le contrat wstETH (la version non-rebasante de stETH, utile pour les integrations DeFi qui preferent un solde constant). Rien n'a ete installe, compile, deploye ni execute pour ecrire ces chapitres. Aucun test n'a ete lance ; ces chapitres decrivent ce que le code Solidity dit faire, en renvoyant aux fichiers cites. Le depot fournit ses propres suites de tests Hardhat et Foundry pour verification independante.
