# clint - chess live interface
clint is a complete website for live broadcasting of a chess tournament based on [pgn4web][2]. It is inspired by many chess websites and strives to offer their best functionalities to any chess broadcast operator. It can also be used simply as a viewer for PGN files.

Single board view | Multiple boards view
:---:|:---:
![interface screenshot][1a] | ![interface screenshot][1b]

Checkout the [demo page][6] to see clint in action.

### Table of contents
* [Usage](https://github.com/pnikic/clint#usage)
    + [Setup](https://github.com/pnikic/clint#setup)
    + [Customization](https://github.com/pnikic/clint#customization)
* [Notes](https://github.com/pnikic/clint#notes)
    + [Credits and license](https://github.com/pnikic/clint#credits-and-license)
    + [Deployments](https://github.com/pnikic/clint#deployments)
    + [Future work](https://github.com/pnikic/clint#future-work)
    + [Donate](https://github.com/pnikic/clint#donate)


### Features
* Banner with general information (about the tournament) and footer with customizable buttons for hyperlinks (other websites, photo gallery, tournament regulations etc.) 
* Chess board with compactly displayed player names, clock times and ratings
* PGN section for display and navigation
* Engine analysis
* Switching between different games and PGN files (rounds) on the same page
* Support for embedding video (live stream) or image for each PGN file (round)
* Download PGN / FEN of the current game, round or whole tournament, sharing link to a specific game
* Multiple boards view (e.g. 6 boards)
* Responsive design - mobile phone friendly
* Full color customization support, predefined light and dark theme

## Usage
### Setup
* Clone this repository on your web server
* Download [pgn4web][2] on your web server
* Edit the `pgn4web.js` path and the fonts path in `index.html` and in `mosaic-tile.html`  
(in my case, pgn4web-3.04 is placed one directory up)
```html
<script src="../pgn4web-3.04/pgn4web.js" defer></script>
...
<link rel="stylesheet" type="text/css" href="../pgn4web-3.04/fonts/pgn4web-font-ChessSansUsual.css">
```
and the image path for the pieces in `assets/js/config.js`
```javascript
SetImagePath("../pgn4web-3.04/images/svgchess");
```

* Upload / broadcast your PGN files on the server, and define their locations in `assets/js/config.js` in the `listPGNFiles()` function. Detailed explanation of all parameters is located through comments in the file itself. A configuration example follows:
```javascript
function listPGNFiles() {
    // If broadcasting a tournament
    allPGNs.push({
        "name" : "Round 1",
        "pgn" : "pgn/r1.pgn"
    });
    allPGNs.push({
        "name" : "Round 2",
        "pgn" : "pgn/r2.pgn"
    });
    // ...
    allPGNs.push({
        "name" : "Archive",
        "pgn" : "pgn/all.pgn"
    });

    // And/or if you just want to display some PGN files (ended tournaments)
    allPGNs.push({
        "name" : "Tournament (last year's edition)",
        "pgn" : "pgn/last_year.pgn",
        "video-left" : "https://www.youtube.com/embed/<your-code>",
        "video-right" : "https://www.youtube.com/embed/<your-code>",
        "image-left" : "<image-url>",
        "image-right" : "<image-url>"
    });
    // ...
}
```
### Customization
In `index.html` you can:
* edit the general information about the tournament (e.g. banner)

In `assets/js/config.js` you can:
* in `operatorSettings()` edit hyperlinks. Detailed explanation of all parameters is located through comments in the file itself. For instance:
```javascript
footerLinks.push({
    "text" : "Photo Gallery",
    "link" : "https://www.example.com",
    "fa-icon" : "fas fa-images"
});
``` 
* some default options (such as autoplay delay, move highlighting etc.)
* expected round duration (used for automatically choosing the initial PGN file to be opened)
* number of miniboards for the multiple boards view
```javascript
let numberMiniboards = 6;
```

In `assets/style.css` you can configure all the colors used on the page. It comes with a predefined light and dark theme.
```css
/* Light theme example preset */
:root {
    --bg-color: #eee;
    --bg-color-text: #111;
    --bg-color-light: #ddd;
    --bg-color-light-text: #111;
    --bg-color-text-light: #888;
    --bg-color-hover: #27c;
    --bg-color-hover-text: #eee;
    --bg-color-active: #cde;
    --main-color-bg: #ddd;
    --main-color-text: #000;
    --main-color-hover: #cccf;
    --main-color-border: #bbb;
    --white-square: #f0d9b5;
    --black-square: #b58863;
    --highlight-white-sq: #cdd26a;
    --highlight-black-sq: #aaa23a;
}
```

## Notes
* The page is currently in Croatian. With little effort, it can be translated to any language
* The repository includes sample PGN files from the [42nd Chess Olympiad][4], which are present only for illustrational and testing purposes. PGN files include
  * r1.pgn - 40 games
  * r2.pgn - 144 games
  * r3.pgn - 596 games
  * all.pgn - 7426 games

### Credits and license
* This website is based on [pgn4web][2]
* The engine currently used is Stockfish compiled to JavaScript. The release is obtained from [stockfish.js][3]
* Icons present on the website are from [Font Awesome][5]
* The layout of components is inspired by [lichess][10]
* The above items remains subject to their original licenses (if any)
* Remaining clint code is Copyright (c) 2020 Patrick Nikić (see [LICENSE][7] file)
* You are free to use clint for your website. You are encouraged to notify me if you are using clint

I hereby sincerely thank all the people who reviewed this page and gave comments or suggestions. Your feedback is much appreciated.  

### Deployments
* [Croatian Individual Championship 2020][13]
* Several pages on [chesscout.info][11], e.g. [Games from chess tournaments in BiH][12], [Sarajevo Club Championshio][14] and [BiH Junior championships 2021][15]
* [Croatia Grand Chess Tour][16]
* Croatian Individual Junior Championships [2021][17], [2020][18], [2019][19] -- here you can see the evolution of Clint over time :)

### Future work:
* Translation
* Stockfish
  * Move to newer version (WASM)
  * Add evaluation bar on the left side
* Clock countdown
  * Add custom color
  * Fix interaction with board rotation (up to 1 second delay)
* Resizable board
* Fix some responsive design issues (regarding rotations to mobile phone)
* Tournament table
* Analysis board
* Add country flags for players
* Add landing page (with countdown to tournament start, description, overview - multiple boards)
* Fetching ratings from FIDE (or link to a player's profile by clicking on the name)
* Placeholder for notifications (e.g. below banner)
* Support for multiple tournaments (when there are too many PGN files, the dropdown menu is not a good option)
* Show which games have new moves

### Donate
If you want to support my work, consider a small donation via [PayPal][8]. Thank you!

[1a]: https://i.imgur.com/m1r2dgu.png
[1b]: https://i.imgur.com/anwWrzE.png
[2]: http://pgn4web.casaschi.net/
[3]: https://github.com/niklasf/stockfish.js
[4]: https://en.wikipedia.org/wiki/42nd_Chess_Olympiad
[5]: https://fontawesome.com/
[6]: http://hrvatski-sahovski-savez.hr/ftp/sucelje_patrick/
[7]: https://github.com/pnikic/clint/blob/master/LICENSE
[8]: https://www.paypal.com/paypalme/pnikic
[10]: https://lichess.org/
[11]: https://www.chessscout.info/
[12]: https://www.chessscout.info/ftp/premijer-liga-BiH/
[13]: https://hrvatski-sahovski-savez.hr/ftp/CroCh2020/
[14]: https://www.chessscout.info/live/prvenstvo-sk-sarajevo/
[15]: https://www.chessscout.info/live/21-kad-jun-prvenstvo-bih-2021/
[16]: https://live.cgct.eu/
[17]: https://hrvatski-sahovski-savez.hr/ftp/PHjuniori2021/
[18]: https://hrvatski-sahovski-savez.hr/ftp/PHjuniori2020/
[19]: https://hrvatski-sahovski-savez.hr/ftp/PHjuniori2019/
