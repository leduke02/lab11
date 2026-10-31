# Error table

One row per failure. Fill in every column. You need at least eight rows.

| Scenario | Function that detects it | Error value | What the player sees |
|---|---|---|---|
| Fleet file does not exist | `load_fleet` | `Err(DataError::Io(..))` (kind `NotFound`) | `Error: could not load data/fleet.txt: <message>`, program exits with code 1 |
| A folder is given as the fleet path | `load_fleet` | `Err(DataError::Io(..))` | `Error: could not load data: <message>`, exit code 1 |
| Fleet file has only comments | `load_fleet` | `Err(DataError::NoShips(path))` | `Error: could not load data/fleet_empty.txt: <message>`, exit code 1 |
| Every line in the fleet file is bad | `load_fleet` | `Err(DataError::NoShips(path))` | `Error: could not load data/fleet_all_bad.txt: <message>`, exit code 1 |
| Board file has nine rows | `parse_board`, called by `load_board` | `Err(DataError::Board(BoardError::WrongRowCount(9)))` | `Practice board unavailable: <message>`, then the menu |
| Board file has a bad character | `parse_board`, called by `load_board` | `Err(DataError::Board(BoardError::BadChar { line: 6, ch: 'x' }))` | `Practice board unavailable: line 6 ...`, then the menu |
| Scores file is missing | `load_scores` | `Ok(vec![])`, not an error | The menu says `no scores yet` |
| Scores file cannot be written | `append_score` | `Err(DataError::Io(..))` | `Could not save the score: <message>`, then the menu |
| `K11` typed at the prompt | `parse_coord` | `Err(CoordError::ColumnOutOfRange('K'))` | `column K is off the board (A–J)`, asked again, no shot counted |

Scenarios to cover (add more if you find them):

- fleet file missing
- a directory given as the fleet path
- fleet file with only comments
- fleet file where every line is bad
- board file with nine rows
- board file with a bad character
- scores file missing
- scores file that cannot be written
- `K11` typed at the prompt
