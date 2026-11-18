# Tiny Chess 4K

An original 4 KB chess engine in a single Python file, written for the
make.fun `tiny-chess-01` bounty. Standard library only. No model calls,
no clock, no randomness: every move uses the same fixed node budget, so
replays are deterministic.

How it plays:

- 0x88 board, full legal move generation: castling, en passant,
  promotion, check evasion.
- Negamax alpha-beta search with iterative deepening to a fixed budget
  of 50,000 nodes per move.
- Quiescence search over captures and promotions, with full evasions
  when in check.
- Evaluation is material plus piece-square tables: advancing centre
  pawns, centralised pieces, and a safe back-rank king.
- Move ordering by static evaluation at the root and MVV-LVA inside
  the search.

It speaks the harness protocol only: `POST /game`, `POST /move`,
`POST /resign` against `MAKEFUN_ENV_URL`, with UCI moves.

`main.py` is at most 4,096 bytes. License: MIT, see `LICENSE`.
