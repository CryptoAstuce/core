# Chapitre 3 — stETH, le jeton rebasant a base de parts

`StETH.sol` n'implemente pas un ERC-20 classique. En interne, chaque detenteur possede un nombre de « parts » (`shares`) fixe, et son solde affiche `balanceOf` se calcule a la volee : `shares[compte] * totalPooledEther / totalShares`.

Quand le protocole rapporte de nouvelles recompenses (ou une perte), seul `totalPooledEther` change ; les parts de chaque detenteur restent identiques. Le solde en stETH de tout le monde augmente donc simultanement et proportionnellement, sans qu'aucune transaction individuelle ne soit necessaire : c'est le « rebasement ». Un exemple donne dans le code : si `user1` a 100 parts et `user2` a 400 parts pour un total de 500 parts et 10 ETH controles, `balanceOf(user1)` vaut 2 stETH et `balanceOf(user2)` vaut 8 stETH.

`getSharesByPooledEth` et `getPooledEthByShares` font les conversions dans les deux sens ; ce sont ces fonctions, et non une simple lecture de solde, que les integrations externes doivent utiliser pour tout calcul precis, car le solde en stETH d'un compte peut varier legerement a chaque rapport d'oracle par arrondi.

`transfer` et `transferFrom` operent en apparence sur des montants de stETH, mais convertissent en interne vers des parts avant de deplacer la valeur : c'est `getSharesByPooledEth(_amount)` qui est reellement transfere, et un evenement `TransferShares` complete le `Transfer` standard pour exposer ce detail aux integrateurs qui en ont besoin.

[Chapitre suivant : le depot (submit) et la limite de stake](04-le-depot-submit.md)
