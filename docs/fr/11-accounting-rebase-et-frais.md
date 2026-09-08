# Chapitre 11 — Accounting : rebase, frais et sanity checks

Une fois un rapport valide par le consensus, `Accounting.handleOracleReport` traduit les nouveaux chiffres de la couche de consensus (solde total des validateurs, validateurs sortis, ether en attente) en changements d'etat concrets pour le protocole.

`_calculateWithdrawals` determine combien de requetes de la file de retraits peuvent etre finalisees avec l'ether disponible ce cycle. `_calculateProtocolFees` et `_calculateFeeDistribution` calculent la part des nouvelles recompenses qui revient au protocole (frais partages entre le tresor de la DAO et les operateurs de noeuds), frappee comme de nouvelles parts de stETH plutot que prelevee en ether — ce qui dilue legerement tous les detenteurs au profit des beneficiaires des frais, sans transaction separee.

`_sanityChecks` est la ligne de defense principale contre un rapport errone ou malveillant : elle verifie que les variations de solde (positives ou negatives) restent dans des bornes raisonnables par rapport au cycle precedent, avant d'appliquer quoi que ce soit. Un rapport qui depasserait ces bornes est rejete plutot qu'applique, meme s'il a atteint le quorum du consensus — une seconde ligne de defense independante du vote des oracles.

`_notifyRebaseObserver` previent les contrats externes abonnes (notamment `TokenRateNotifier`) qu'un rebasement vient d'avoir lieu, pour que les integrations qui dependent du taux de change stETH/ETH (comme des oracles de prix sur d'autres chaines) puissent se mettre a jour.

[Chapitre suivant : le burner et les parts brulees](12-le-burner.md)
