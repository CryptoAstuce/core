# Chapitre 5 — Le tampon d'ether et ses reserves

L'ether depose n'est pas immediatement mis en jeu : il s'accumule dans un tampon (`buffer`) en attendant d'etre reparti par le routeur de staking. `_getBufferedEtherAllocation`, dans `Lido.sol`, decoupe ce tampon en trois zones par ordre de priorite, documente par un schema ASCII directement dans le code source.

La `depositsReserve` est remplie en premier : c'est l'allocation de depot disponible pour la couche de consensus a chaque periode, reconstituee a chaque rapport d'oracle. La `withdrawalsReserve` vient ensuite : elle couvre exactement le montant de stETH en attente de retrait non encore finalise (`unfinalizedStETH`), et n'est jamais mise en jeu tant que ces retraits ne sont pas satisfaits. Ce qui reste, l'`unreserved`, est l'exces disponible pour des depots supplementaires au-dela de l'allocation courante.

Cet ordre de priorite traduit un choix de conception explicite : le protocole garantit d'abord la liquidite necessaire aux utilisateurs qui attendent de retirer leurs fonds, avant de chercher a maximiser la part de l'ether mise en jeu pour les recompenses.

`withdrawDepositableEther` retire du tampon la part reellement disponible pour le depot et la transmet au `StakingRouter`, qui se charge de la repartition entre modules d'operateurs.

[Chapitre suivant : le staking router et les modules d'operateurs](06-le-staking-router-et-les-modules.md)
