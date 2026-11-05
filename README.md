# TIS-100 Bench

**TIS-100 Bench: LLMs Push the Pareto Frontier in Programming Puzzle Games.** [Read the article](https://tis-100.wincon.dev/).

16 LLMs played all 47 puzzles of the programming game [TIS-100](https://www.zachtronics.com/tis-100/) plus 8 community tournament puzzles (55 in all), with 10 to 45 minutes per puzzle and no access to the community leaderboard. They found **133 new Pareto-frontier points on 18 of 55 puzzles**, including **3 outright cycle records**. This release has all 3,714 programs on the models' Pareto frontiers, with their scores.

Also on Hugging Face: [wincon-research/tis100-bench](https://huggingface.co/datasets/wincon-research/tis100-bench) (programs and scores as a table).

## Leaderboard

| # | Model | Puzzles with new frontier points | Solved | Record proximity |
|---:|---|---:|---:|---:|
| 1 | Opus 5.5 | 11 | 55 / 55 | 77.2 |
| 2 | GPT-6 Astra | 11 | 55 / 55 | 78.0 |
| 3 | Gemini 4 Argon | 8 | 54 / 55 | 76.2 |
| 4 | Sonnet 5.5 | 7 | 53 / 55 | 69.9 |
| 5 | GPT-6.1 Sol | 6 | 54 / 55 | 75.6 |
| 6 | Fable 5.1 | 5 | 52 / 55 | 70.2 |
| 7 | Kimi K3.1 Pro | 2 | 52 / 55 | 64.6 |
| 8 | Gemini 3.8 Flash | 1 | 53 / 55 | 66.0 |
| 9 | Muse Wonder 1.0 | 1 | 49 / 55 | 58.8 |
| 10 | Haiku 5.5 | 1 | 45 / 55 | 53.7 |
| 11 | GLM-5.3 | 1 | 30 / 55 | 35.5 |
| 12 | Grok 4.7 | 0 | 44 / 55 | 50.1 |
| 13 | DeepSeek V4.1 Flash | 0 | 40 / 55 | 46.8 |
| 14 | Muse Spark 1.3 | 0 | 39 / 55 | 45.1 |
| 15 | gpt-6-luna | 0 | 39 / 55 | 42.8 |
| 16 | MiMo-V2.6-Pro | 0 | 10 / 55 | 12.8 |

Snapshot `2026-11-03-v5`, one attempt per model and puzzle.

## Highlight

On the tournament puzzle Undecimal Twin Rounder (`SPEC44149538`), Opus 5.5 cut the community cycle record from 2,694 to
1,918 (`programs/SPEC44149538/opus/SPEC44149538.1918-8-88.txt`). A player then took that program to 1,744; the leaderboard now credits
LongingForRest/opus-5-5.

## Files

- `programs/<puzzle>/<model>/<puzzle>.<cycles>-<nodes>-<instructions>.txt`: one file per program, in TIS-100 save
  format and named like the community leaderboard's files.
- `points.csv`: every program with its puzzle, model, scores and whether it is a new frontier point.
- `models.csv`: the leaderboard above.

## Method

Each model had one scored attempt per puzzle (pass@1): find a working program, then keep improving it on
all three of the game's scores (cycles, nodes, instructions). Time limits were 10, 30 and 45 minutes for easy, medium
and hard puzzles. Models had no access to the community leaderboard.

Every program on a model's final Pareto frontier was replayed in a fresh game and run against 100,000 random test
inputs in [TIS-100-CXX](https://github.com/killerbee13/TIS-100-CXX). A point counts as a **new frontier point** when it passed all of those tests and no
program on the [community leaderboard](https://github.com/12345ieee/tis100-leaderboard) (frozen at commit `e311401`) is as good or better
on all three scores. **Record proximity** is the community's best score divided by the model's best, averaged over the
three scores and all 55 puzzles (×100; unsolved puzzles count as 0).

186 rows are flagged as new frontier points. Different models sometimes found the same point, or one model's
point beats another's, so the combined frontier has 133 distinct new points.

Full methods, analysis and an interactive Pareto explorer are in the [article](https://tis-100.wincon.dev/).

## Run a program

Built-in puzzles are recognised from the file name. Community tournament puzzles (`SPEC…`) need their
Lua spec from the [leaderboard bot](https://github.com/F43nd1r/zachtronics-leaderboard-bot/tree/master/src/main/resources/tis/custom) and a TIS-100-CXX build with Lua support.

```sh
TIS-100-CXX -r 100000 programs/00150/opus/00150.83-8-8.txt
TIS-100-CXX -L 44149538.lua -r 100000 programs/SPEC44149538/opus/SPEC44149538.1918-8-88.txt
# validation successful
# score: 1918/8/88
```

## License and credit

MIT. Credit programs as "Wincon (model name)". TIS-100 is a trademark of Zachtronics; this project is not affiliated
with or endorsed by Zachtronics.

Research teams can ask us for the RL environment and episode traces: hello@wincon.dev.

## Citation

```bibtex
@misc{wincon2026tis100bench,
  title  = {TIS-100 Bench: LLMs Push the Pareto Frontier in Programming Puzzle Games},
  author = {{Wincon}},
  year   = {2026},
  month  = nov,
  url    = {https://tis-100.wincon.dev/},
  note   = {Benchmark snapshot 2026-11-03-v5}
}
```
