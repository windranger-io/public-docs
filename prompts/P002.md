# Improving Wallet Interactions with Native Games

_from jacobc.eth of_ [_`Game7`_](https://game7.io/)

## Prompt

#### Background&#x20;

Currently, web3 game developers are forced to choose between building a browser game with great wallet compatibility by building a webGL game (where games are laggy and graphical performance is limited), or to launch as a native desktop or mobile game with virtually no transactions and instead push all transactional activity to a separate web application. Some projects are forced to launch their own proprietary wallets to get around this problem, only to find that their wallets aren’t interoperable with other web3 sites and games, so assets remain stuck in silos.

#### Scope&#x20;

We are seeking the best technical approach and implementation for passing through and overlaying a natively installed wallet (Ie. MetaMask or another natively installed wallet) on top of a native desktop game.

#### Suggestions&#x20;

A number of existing native applications engage in the sort of overlay heavior, for example, Steam or Discord. Some have suggested that the technical approach of libraries like [goverlay](https://github.com/hiitiger/goverlay/blob/master/README.md) or [MangoHUD](https://github.com/flightlessmango/MangoHud) could be replicated for these purposes.

#### Requirements&#x20;

* Any solution must be able to prevent the native game from tampering with the overlaid UI elements. If a game can potentially force the player’s private keys to consent to a transaction that the player didn’t consent to, the solution is disqualified.&#x20;
* BONUS: Allow the player to hide and unhide the wallet UI layer through a hotkey interaction similar to Steam&#x20;
* BONUS: Enable the game to initiate a transaction request, similar to a web3 site requesting a transaction approval from MetaMask&#x20;

## Submission or feedback&#x20;

Please email: [jacob@game7.io](mailto:jacob@game7.io)
