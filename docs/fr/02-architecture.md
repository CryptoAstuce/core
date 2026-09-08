# Chapitre 2 — Architecture du depot

`contracts/0.4.24/` contient les contrats historiques les plus anciens : `Lido.sol` (le contrat central, herite d'une architecture Aragon), `StETH.sol` (le jeton rebasant), et `nos/NodeOperatorsRegistry.sol` (le premier module d'operateurs de noeuds).

`contracts/0.8.9/` contient les briques ajoutees ensuite : `WithdrawalQueue.sol` et `WithdrawalQueueBase.sol` (la file d'attente de retraits), `Burner.sol` (le contrat qui brule des parts de stETH pour couvrir des pertes), `Accounting.sol` (le calcul des rapports d'oracle), `LidoLocator.sol` (l'annuaire des adresses des contrats du protocole), et le dossier `oracle/` (consensus et rapport de la couche de consensus).

`contracts/0.8.25/` contient les ajouts les plus recents : `sr/StakingRouter.sol` (le routeur multi-modules) et un dossier `vaults/` experimental pour une architecture de coffres de staking plus recente, hors du perimetre principal de ce parcours.

`LidoLocator.sol` joue un role particulier : plutot que de coder en dur les adresses des contrats satellites (routeur, burner, file de retraits, oracle...), chaque contrat interroge le `Locator` a l'execution. Cela permet de remplacer un composant sans redeployer tout le protocole.

[Chapitre suivant : stETH, le jeton rebasant a base de parts](03-steth-le-jeton-rebasant.md)
