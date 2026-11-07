# Test plans

One file per test, written before the flight. Naming: `TP-NNN_short-description.md`

## Template

```markdown
# TP-NNN: <title>

| | |
|---|---|
| Date planned | |
| Parameter set | params/<file> |
| Location | indoor / outdoor, airspace category |
| Weather limits | max. wind, no rain |

## Objective
What question does this test answer?

## Configuration
Hardware changes, propellers, battery, relevant parameters.

## Procedure
1. ...
2. ...

## Data to record
ULog profile, additional measurements (scale, stopwatch, voltage after landing).

## Success criteria
Measurable, e.g. "roll step response overshoot < 10 %".

## Abort criteria
e.g. oscillation, motor temperature, unexpected mode change, battery < 3.5 V/cell under load.

## Risks and mitigation
```

## Index

| ID | Title | Status | Report |
|---|---|---|---|
| | | | |
