# Chapitre 7 — Le registre des node operators

`NodeOperatorsRegistry.sol`, dans `contracts/0.4.24/nos/`, est le premier et le plus etabli des modules de staking : chaque operateur de noeud enregistre y depose des cles de validation publiques et des signatures, que le protocole utilise pour deployer de nouveaux validateurs.

`addSigningKeys` permet a un operateur d'ajouter des cles a son quota ; `setNodeOperatorStakingLimit` (appele « vetted signing keys count ») fixe combien de ces cles la DAO a effectivement approuvees et rendues eligibles au depot — une cle ajoutee par l'operateur n'est pas utilisee tant qu'elle n'a pas ete « vettee ».

Le suivi du cycle de vie d'un validateur passe par plusieurs compteurs par operateur : cles deposees, cles vettees, validateurs actifs, validateurs sortis (`updateExitedValidatorsCount`). `decreaseVettedSigningKeysCount`, appelable par le `StakingRouter`, permet de retirer des cles de la file si un operateur est juge a risque, sans toucher aux validateurs deja actifs.

Ce module n'est qu'une implementation parmi celles que le `StakingRouter` peut orchestrer ; d'autres modules, avec d'autres regles de permission ou d'autres mecanismes de garantie, peuvent coexister avec lui, chacun etant un contrat separe respectant la meme interface attendue par le routeur.

[Chapitre suivant : la file d'attente de retraits](08-la-file-de-retraits.md)
