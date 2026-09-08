# Chapitre 9 — Finalisation des retraits et les checkpoints

Finaliser une requete de retrait signifie lui garantir un montant d'ether reclamable, fige a un taux de change stETH/ETH donne. `_finalize`, dans `WithdrawalQueueBase.sol`, avance le curseur de la derniere requete finalisee et verrouille l'ether necessaire (`_setLockedEtherAmount`), sans transferer immediatement les fonds a chaque utilisateur individuellement.

Le taux de change applique n'est pas necessairement le taux courant : `_maxShareRate` plafonne le taux utilise pour la finalisation, une protection contre le fait de payer les retraits a un taux plus favorable que celui reellement disponible si le protocole a subi une perte depuis la demande.

Chaque finalisation cree un `Checkpoint` : un couple (identifiant de premiere requete concernee, taux de change applique). Comme le taux peut differer d'une finalisation a l'autre, retrouver le taux exact applique a une requete donnee demande une recherche parmi les checkpoints — `findCheckpointHints` fournit cette recherche par dichotomie, et le resultat (le « hint ») est passe en parametre a `claimWithdrawal` pour eviter de la refaire on-chain a chaque reclamation.

Ce decouplage entre finalisation (par lots, potentiellement a des taux differents) et reclamation (individuelle, via un hint precalcule) permet de finaliser un grand nombre de requetes en une seule transaction sans faire exploser son cout en gaz.

[Chapitre suivant : le consensus et le rapport d'oracle](10-consensus-et-rapport-oracle.md)
