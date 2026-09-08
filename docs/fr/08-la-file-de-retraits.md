# Chapitre 8 — La file d'attente de retraits

`WithdrawalQueue.sol` et `WithdrawalQueueBase.sol` gerent les demandes de retrait : un detenteur de stETH (ou de wstETH, sa version non-rebasante) verrouille son solde en echange d'une position dans une file FIFO, en attendant qu'elle soit financee et finalisee.

Chaque requete est stockee comme un point sur une courbe cumulative : `cumulativeStETH` et `cumulativeShares` additionnent, requete apres requete, le montant total demande depuis le debut de la file. Cette structure cumulative permet de calculer le montant exact d'un lot de requetes consecutives par simple soustraction, sans avoir a parcourir chaque requete individuellement.

`requestWithdrawals` accepte un tableau de montants (pas un seul), chacun devenant une requete separee : cela permet a un utilisateur de scinder un gros retrait en plusieurs positions plus faciles a transferer ou revendre independamment, puisque chaque requete est representee par un NFT (`WithdrawalQueueERC721`).

`unfinalizedStETH` renvoie le montant total encore en attente de financement dans la file : c'est cette valeur qui alimente directement la `withdrawalsReserve` du tampon d'ether calculee au chapitre precedent.

[Chapitre suivant : finalisation des retraits et les checkpoints](09-finalisation-et-checkpoints.md)
