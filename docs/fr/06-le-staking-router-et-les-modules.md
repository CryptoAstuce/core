# Chapitre 6 — Le staking router et les modules d'operateurs

`StakingRouter.sol` repartit l'ether disponible entre plusieurs « modules de staking » enregistres, chacun representant une facon differente d'operer des validateurs (le registre classique d'operateurs geres par la DAO, mais aussi potentiellement des modules communautaires ou sans permission).

Chaque module a un `stakeShareLimit` (la part maximale du total mis en jeu qu'il peut recevoir) et un `priorityExitShareThreshold` (le seuil au-dela duquel ses validateurs deviennent prioritaires pour la sortie en cas de besoin de liquidite). `addStakingModule` et `updateStakingModule`, reserves au role `STAKING_MODULE_MANAGE_ROLE`, permettent a la gouvernance d'ajuster ces parametres ou d'ajouter de nouveaux modules sans toucher au contrat `Lido` central.

`topUp` est la fonction qui effectue reellement les depots aupres du contrat de depot Ethereum officiel, module par module, dans la limite du nombre de cles de validation disponibles et vetees pour chaque module (`getStakingModuleMaxDepositsCount`).

Le routeur centralise aussi la remontee d'information : `reportRewardsMinted`, `updateExitedValidatorsCountByStakingModule` et les fonctions de rapport de solde par module servent de point de passage unique entre l'oracle de comptabilite et chaque module, qui garde son propre etat interne de validateurs.

[Chapitre suivant : le registre des node operators](07-le-registre-des-node-operators.md)
