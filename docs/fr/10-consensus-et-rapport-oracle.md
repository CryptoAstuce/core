# Chapitre 10 — Le consensus et le rapport d'oracle

Le contrat `Lido` ne connait rien de la couche de consensus Ethereum par lui-meme : un ensemble d'oracles off-chain surveille les soldes et le statut des validateurs, et rapporte periodiquement cet etat on-chain via `AccountingOracle.sol`, dans `contracts/0.8.9/oracle/`.

`HashConsensus.sol` organise le vote : plusieurs oracles independants soumettent chacun le hash du rapport qu'ils ont calcule pour une periode (« reference slot ») donnee ; seul un rapport ayant atteint un quorum de membres est retenu. Ce mecanisme de consensus multi-parties evite qu'un oracle unique, corrompu ou en panne, ne puisse imposer un etat errone au protocole.

`submitReportData` accepte ensuite les donnees completes correspondant au hash qui a atteint le quorum ; `getCurrentFrame` et `getProcessingState` exposent l'etat d'avancement du cycle de rapport courant, utile pour les oracles eux-memes et pour la supervision externe.

Le rapport peut aussi porter des « donnees supplementaires » (`extra data`), soumises separement via `submitReportExtraDataList`, pour des informations volumineuses comme le detail des validateurs sortis par operateur, qui ne tiennent pas dans le rapport principal sans depasser les limites de gaz d'une transaction.

[Chapitre suivant : accounting : rebase, frais et sanity checks](11-accounting-rebase-et-frais.md)
