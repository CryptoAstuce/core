# Chapitre 12 — Le burner et les parts brulees

`Burner.sol` est un contrat dedie a une seule operation : bruler des parts de stETH de facon permanente, en dehors du chemin normal de retrait.

Cette fonction sert principalement a « couvrir » des pertes exceptionnelles constatees sur la couche de consensus (par exemple des penalites severes appliquees a des validateurs). Plutot que de laisser la perte diluer silencieusement tous les detenteurs de stETH via un simple ajustement du `totalPooledEther`, le protocole peut choisir de la faire porter specifiquement par une reserve de shares dediee, en la brulant : `requestBurnSharesForCover` et `requestBurnMyStETHForCover` enregistrent une demande de brulage « pour couverture », distincte des brulages ordinaires.

Les demandes de brulage passent par une file d'attente interne au contrat plutot que d'etre executees immediatement : `Accounting.sol` les traite au rythme des rapports d'oracle, dans le cadre du calcul global de rebase du cycle, pour que l'effet du brulage et celui du rapport de recompenses soient coherents entre eux plutot que d'entrer en conflit.

`recoverExcessStETH`, `recoverERC20` et `recoverERC721` sont des fonctions de secours qui permettent de recuperer des jetons envoyes par erreur au contrat, distinctes du mecanisme de brulage volontaire qui est, lui, definitif et sans recuperation possible.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
