# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/arukh89/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/arukh89/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 4 KB chess engine in a single Python file, written for the
make.fun `tiny-chess-01` bounty. Standard library only. No model calls,
no clock, no randomness: every move uses the same fixed node budget, so
replays are deterministic.

How it plays:

- 0x88 board, full legal move generation: castling, en passant,
  promotion, check evasion.
- Negamax alpha-beta search with iterative deepening to a fixed budget
  of 50,000 nodes per move, with killer moves, a transposition table
  that persists across moves, and an in-search repetition shortcut.
- Quiescence search over captures and promotions, with full evasions
  when in check.
- Evaluation is material plus piece-square tables: advancing centre
  pawns, centralised pieces, a safe back-rank king, and separate rook
  and queen piece-square tables.
- Move ordering by static evaluation at the root and MVV-LVA inside
  the search.

It speaks the harness protocol only: `POST /game`, `POST /move`,
`POST /resign` against `MAKEFUN_ENV_URL`, with UCI moves.

`main.py` is packed from its readable source with `makefun compress`
and is at most 4,096 bytes. License: MIT, see `LICENSE`.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 -P -s main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
