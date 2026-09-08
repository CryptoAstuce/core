# Chapitre 1 — Presentation de Lido

Lido est un protocole de liquid staking sur Ethereum : il permet de miser de l'ether pour toucher les recompenses du staking sans immobiliser ses fonds ni faire tourner soi-meme un validateur.

Le mecanisme central est le jeton `stETH`. Deposer de l'ether donne du stETH en echange, un jeton dont le solde suit automatiquement les recompenses (et les penalites) accumulees par les validateurs sous-jacents. Contrairement a un depot classique de 32 ETH sur le contrat de depot Ethereum, Lido accepte des montants de n'importe quelle taille et mutualise les fonds de tous les deposants.

Ce depot, `lidofinance/core`, contient le coeur du protocole : le contrat `Lido` lui-meme, le jeton `stETH`, le routeur de staking qui repartit les fonds entre plusieurs modules d'operateurs de noeuds, la file d'attente de retraits, et les contrats d'oracle qui rapportent l'etat de la couche de consensus.

Le code melange plusieurs versions de Solidity dans des dossiers separes (`0.4.24`, `0.8.9`, `0.8.25`) : c'est l'historique du protocole, deploye et mis a niveau progressivement depuis son lancement, chaque nouvelle brique ajoutee dans la version de compilateur en cours a l'epoque.

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : architecture du depot](02-architecture.md)
