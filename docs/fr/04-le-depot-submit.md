# Chapitre 4 — Le depot (submit) et la limite de stake

`submit(_referral)` est le point d'entree pour deposer de l'ether : il accepte n'importe quel montant non nul, calcule le nombre de parts correspondant via `getSharesByPooledEth(msg.value)`, les attribue au deposant, et ajoute le montant au tampon (`buffer`) d'ether en attente de mise en jeu.

Une fonction de secours (`fallback`) redirige tout envoi d'ether brut vers `_submit(0)`, a condition qu'aucune donnee ne soit jointe a l'appel — une protection contre les envois accidentels vers une fonction inexistante.

Le depot est soumis a une limite de debit (`stake limit`) geree par `setStakingLimit` : un plafond maximal et un taux de reconstitution par bloc, un mecanisme de type « seau perce » qui protege le protocole d'un afflux soudain et massif de depots qui deséquilibrerait la repartition entre modules d'operateurs avant le prochain rapport d'oracle. `pauseStaking` et `resumeStaking` permettent de couper entierement les nouveaux depots en cas d'urgence.

Chaque depot declenche `_emitTransferAfterMintingShares`, qui emet un evenement `Transfer` standard depuis l'adresse zero, pour que les indexeurs et portefeuilles qui suivent uniquement les evenements ERC-20 classiques voient bien apparaitre le nouveau solde de stETH.

[Chapitre suivant : le tampon d'ether et ses reserves](05-le-tampon-et-ses-reserves.md)
