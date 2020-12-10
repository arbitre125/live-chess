# clint - chess live interface
clint is a complete website for live broadcasting of a chess tournament based on [pgn4web][2]. It is inspired by many chess websites and strives to offer their best functionalities to any chess broadcast operator. It can also be used simply as a viewer for PGN files.

Single board view | Multiple boards view
:---:|:---:
![interface screenshot][1a] | ![interface screenshot][1b]

A demo is available on: http://hrvatski-sahovski-savez.hr/ftp/sucelje_patrick/

### Features
* Banner with general information (about the tournament) and customizable buttons for hyperlinks (other websites, photo gallery, tournament regulations etc.) 
* Chess board with compactly displayed player names, clock times and ratings
* PGN section for display and navigation
* Engine analysis
* Switching between different games and PGN files (rounds) on the same page
* Support for embedding video (live stream) for each PGN file (round)
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
<script src="../pgn4web-3.04/pgn4web.js"></script>
...
<link rel="stylesheet" type="text/css" href="../pgn4web-3.04/fonts/pgn4web-font-ChessSansUsual.css">
```
and the image path for the pieces in `assets/js/setup.js`
```javascript
SetImagePath("../pgn4web-3.04/images");
```

* Upload / broadcast your PGN files on the server, and define their locations in `assets/js/setup.js` in the `listPGNFiles()` function. For instance:
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

    // And / or if you just want to display some PGN files (ended tournaments)
    allPGNs.push({
        "name" : "Tournament (last year's edition)",
        "pgn" : "pgn/last_year.pgn"
    });
    // ...
}
```
### Customization
In `index.html` you can:
* edit the general information about the tournament
* add / edit buttons for hyperlinks

In `assets/js/setup.js` you can configure:
* in `operatorSettings()` edit the links to already defined buttons and name of the operator
* some default options (such as autoplay delay, move highlighting etc.)
* number of miniboards for the multiple boards view
```javascript
let numberMiniboards = 6;
```

In `assets/style.css` you can configure all the colors used on the page. It comes with a predefined light and dark theme.

## Notes
* The page is currently in Croatian. With little effort, it can be translated to any language
* The repository includes sample PGN files from the [42nd Chess Olympiad][4], which are present only for illustrational purposes. Each PGN file includes cca. 600 games

## Credits and license
* This website is based on [pgn4web][2]
* The engine currently used is Stockfish compiled to JavaScript. The release is obtained from [stockfish.js][3]
* Icons present on the website are from [Font Awesome][5]
* The layout of components is inspired by [lichess][10]
* The above items remains subject to their original licenses (if any)
* Remaining clint code is Copyright (c) 2020 Patrick Nikić (see [LICENSE][7] file)
* You are free to use clint for your website. You are encouraged to notify me if you are using clint

I hereby sincerely thank all the people who reviewed this page and gave comments or suggestions. Your feedback is much appreciated.  

## Future work:
* Translation
* Add functionality for live time countdown during broadcast
* Resizable board
* Fix some responsive design issues (regarding to mobile phone rotations)
* Searching games by player name

[1a]: https://i.imgur.com/m1r2dgu.png
[1b]: https://i.imgur.com/anwWrzE.png
[2]: http://pgn4web.casaschi.net/
[3]: https://github.com/niklasf/stockfish.js
[4]: https://en.wikipedia.org/wiki/42nd_Chess_Olympiad
[5]: https://fontawesome.com/
[7]: https://github.com/pnikic/clint/blob/master/LICENSE
[10]: https://lichess.org/
