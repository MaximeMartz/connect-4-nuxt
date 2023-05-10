# connect four

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev


## Gameplay

The object of the game is to line up a sequence of 4 pawns of the same color on a grid with 6 rows and 7 columns. Each player has 21 pawns of one color (by convention, usually yellow or red). Alternately, the two players place a pawn in the column of their choice, the pawn then slides to the lowest possible position in the said column after which it is up to the opponent to play. The winner is the player who first achieves a consecutive alignment (horizontal, vertical or diagonal) of at least four pawns of his color. If, while all the squares of the game grid are filled, neither of the two players has made such an alignment, the game is declared void.