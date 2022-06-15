# Wordle Solver
A python program that can solve the Wordle word-guessing game and many of its variants.

## Setup
You may download and install this package using pip
```bash
pip install wordle-autosolver
```

## Usage
Use this module to solve Wordle and other similar puzzles. Default behavior requires the user to interact with the program through the console. This program will use the user's guess and the game's response to filter a list of possible answers. It will then check every possible guess the user could make next, and check the size of the answer list after each possible response. The program will then recommend the guesses which have the smallest worst-case response. The "-auto" flag allows the user to automate the entry of guesses and responses by connecting to websites and interacting with them using chromedriver + selenium. Current supported websites include: [Wordle](www.nytimes.com/games/wordle/index.html), [Dordle](zaratustra.itch.io/dordle), [Quordle](www.quordle.com), [Octordle](octordle.com), [Sedecordle](www.sedecordle.com), [Duotrigordle](duotrigordle.com), [64ordle](64ordle.au), [Nordle](www.nordle.us), [Wordzy](wordzmania.com/Wordzy), and [Fibble](fibble.xyz).
```
python -m wordle-autosolver [-h] [-n N] [-nyt | -hard | -master | -liar] [-best] [-quiet] [-clean]
                            [-auto WEBSITE | -sim MAX_SIMS] [-continue LIMIT | -endless | -challenge]
                            [-start WORD [WORD ...]]

optional arguments:
  -h, --help            show this help message and exit
  -n N                  number of simultaneous games (default: 1)
  -nyt                  only consider answers that are in the New York Times official word list
  -hard                 use if playing on hard mode (default: False)
  -master               only set this flag if the game does not tell you which colors belong to
                        which letters (default: False)
  -liar                 use if playing Fibble where one letter in each response is always a lie
                        (default: False) (currently does not support use with "auto" flag)
  -sim MAX_SIMS         set this flag to simulate MAX_SIMS unique games and give resulting stats
  -best                 set this flag to generate a minimal guess tree (be aware that this process
                        may be very slow)
  -quiet                hide all unnecessary console output
  -clean                empty the contents of "data/best_guess.json", "data/responses.json", and
                        each of their variants to relieve some storage space (the program will not
                        execute any other commands when this flag is set)
  -auto WEBSITE         set this flag to automate play on the given website (requires chromedriver)
                        -- NOTE: websites with a fixed number of boards will override the N
                        argument for number of boards -- valid websites are: 'wordle', 'wordzy',
                        'dordle', 'quordle', 'octordle', 'sedecordle', 'duotrigordle', '64ordle',
                        'nordle', and 'fibble'
  -continue LIMIT       set this flag to continue playing on multiple boards up to the given number
                        (max 500) -- setting the limit to "-1" will test all possible starting
                        words to find the best one(s) (be aware that this process may be very slow)
  -endless              use to play the same game over and over -- when used with "-auto wordzy",
                        will play Wordzy's Maniac mode where the number of games increment by one
  -challenge            play the daily Wordle, Dordle, Quordle, and Octordle in order, using the
                        answers from each puzzle as the starting words for the next (inspired by
                        YouTube channel Scott Stro-solves)
  -start WORD [WORD ...]
                        set this flag if there are certain words you want to start with regardless
                        of the response
```

## Example
```
$ python -m wordle-autosolver -auto wordle -n 4 -start lucky words
Loading precalculated data...
Finished loading.

Connecting to the target website...
Connected to 'https://www.quordle.com/#/'

Starting solver. Simulating 4 simultaneous Wordle games.

Suggested starting word is SALON


Solved  0/4  boards: [*****, *****, *****, *****]

  Predetermined guess is LUCKY

  Response was "....." on board 1
  Best guess(es) on board 1: SANER
    1576 possible answers
  Response was "....." on board 2
  Best guess(es) on board 2: SANER
    1576 possible answers
  Response was "..+.." on board 3
  Best guess(es) on board 3: SHORE
    309 possible answers
  Response was ".O..." on board 4
  Best guess(es) on board 4: TERMS, TREMS
    149 possible answers

Solved  0/4  boards: [*****, *****, *****, *U***]

  Predetermined guess is WORDS

  Response was "+...+" on board 1
  Best guess(es) on board 1: POINT, MEANT, PHASE, SHAPE, PRINT, SAINT, SPITE, PAINT, ...
    18 possible answers
  Response was ".O..+" on board 2
  Best guess(es) on board 2: MEDIA, EMAIL, MERIT, FISTS, THINE, MAIZE, MISTY, AMINE, ...
    18 possible answers
  Response was "...O." on board 3

    The answer on board 3 is CHIDE

  Response was "....O" on board 4
  Best guess(es) on board 4: PETIT, BATHE, INEPT, MOTEN, PATEN, PETTI, MEINT
    34 possible answers

Solved  1/4  boards: [*****, *O***, CHIDE, *U**S]

  Guessing CHIDE...

  Response was "....+" on board 1
  Best guess(es) on board 1: SWEEP
    4 possible answers: SWEET, SWEPT, SWEAT, SWEEP
  Response was "....O" on board 2
  Best guess(es) on board 2: AMONG, ALONG, WRONG, SIGNS, GROWN, SONGS, MASON, AGONY, ...
    4 possible answers: GOOSE, MOOSE, NOOSE, POSSE
  Response was "....+" on board 4
  Best guess(es) on board 4: THUMB, TOMBS, AMBIT, TIMBO
    10 possible answers

Solved  1/4  boards: [SWE**, *O*SE, CHIDE, *U**S]

  Guessing AMBIT...

  Response was "....." on board 1

    The answer on board 1 is SWEEP

  Response was ".+..." on board 2

    The answer on board 2 is MOOSE

  Response was "....." on board 4
  Best guess(es) on board 4: GUESS, FUSES
    2 possible answers: GUESS, FUSES

Solved  3/4  boards: [SWEEP, MOOSE, CHIDE, *U**S]

  Guessing SWEEP...

  Response was "+.O.." on board 4

    The answer on board 4 is GUESS


Solve complete.

Entering all remaining answers... (2 total)
  Entered     1/4    SWEEP
  Entering    2/4    MOOSE
  Entered     3/4    CHIDE
  Entering    4/4    GUESS
Saving all newly discovered data...
Save complete.
PRESS ENTER TO EXIT
```
