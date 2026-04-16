# Chess Text — Chess Text Reasoning

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | Chess Text |
| Creators | Google DeepMind |
| Year Published | 2025 |
| Task Type | Inferring board state from text descriptions |
| Evaluation Dimension | Strategic reasoning capability |
| Scoring System | Bayesian Skill Rating |
| Dataset Link | Kaggle Leaderboard |
| Status | New direction in spatial reasoning evaluation |

## Overview

Chess Text is a chess text reasoning evaluation benchmark developed by Google DeepMind, designed to test AI models' ability to understand spatial relationships and infer board states from natural language descriptions. Unlike traditional chess-playing evaluations, Chess Text does not test board memory or pattern recognition, but rather evaluates models' ability to understand complex spatial relationships and strategic situations through text reasoning.

## Dataset Composition

### Question Format

- Board piece positions and move sequences are described in natural language
- Models are asked to infer the current board state, best moves, or strategic assessments
- No visual chess board is provided; purely text input and output

### Reasoning Types

1. **Spatial Reasoning**: Building a mental board model from text descriptions
2. **Tactical Identification**: Recognizing implicit tactical combinations in the text (fork, pin, skewer, etc.)
3. **Strategic Assessment**: Evaluating position advantages and long-term strategic direction
4. **Move Verification**: Determining whether a given move is legal and optimal

### Difficulty Levels

- Basic: 2-3 move tactical combinations
- Intermediate: 5-8 move tactical sequences
- Advanced: Strategic reasoning across complete games

## Evaluation Method

### Bayesian Skill Rating System

Chess Text employs a Bayesian skill rating system similar to chess Elo ratings:

- Bayesian inference based on Elo rating principles
- Each question has a corresponding difficulty level
- Model ability is estimated through question-answering performance
- Results are reported as Skill Ratings, which can be compared to human chess Elo ratings

### Scoring Dimensions

- **Position Inference Accuracy**: Correctly inferring piece positions
- **Move Quality**: Optimality of suggested moves
- **Strategic Assessment Consistency**: Consistency of position evaluations with strong engine evaluations

## Model Performance (April 2026)

| Model | Chess Text Skill Rating (approx.) | Corresponding Human Level |
|-------|----------------------------------|--------------------------|
| Gemini 3 Pro | ~1800 | Intermediate amateur |
| GPT-5 | ~1700 | Intermediate amateur |
| Claude Opus 4.6 | ~1650 | Lower amateur |
| Human International Master | 2200+ | Master level |
| Human Professional Player | 2500+ | Grandmaster level |

> Note: The above are approximate values; please refer to the Kaggle leaderboard for specific ratings. Skill ratings can be roughly compared to the FIDE Elo rating system.

## Example Tasks

### Spatial Reasoning
```
Description: White King on e1, Queen on d1, Rook on a1 and h1,
Knight on f3, Bishop on c1 and f1, Pawn on d4 and e5.
Black King on e8, Queen on d8, Rook on a8 and f8,
Knight on c6, Bishop on b7, Pawn on d5 and f7.

After White plays Nf3-e5, how should Black respond?

Answer: Black can play ...dxe5 to gain a pawn advantage, or
...Nxe5 to maintain material balance. The better choice is ...Nxe5,
because the d5 pawn maintains central control.
```

### Tactical Identification
```
Description: In the current position, White Queen on b3, Bishop on c4,
Black King on e8, Knight on f6, Pawn on g7.

What tactical threats does White have?

Answer: White's Qb3+Bc4 forms an "Italian Attack" configuration,
threatening Qxf7+ check. Black's Nf6 defends the f7 square,
but if White can drive away the knight (e.g., via g5 pawn push),
White will have a lethal attack.
```

## Variants and Related Benchmarks

### Chess LLM Arena
- LLM-based chess-playing platform
- Tests actual playing ability rather than text reasoning

### Board Game Bench
- Reasoning evaluation covering multiple board games
- Includes Go, chess, and others

### Spatial Reasoning Benchmarks
- General spatial reasoning evaluation
- Not limited to board game scenarios

## Limitations and Controversies

1. **Not a Playing Evaluation**: Tests text reasoning rather than actual playing ability; the two capabilities may not be consistent
2. **Board Representation Bias**: Text descriptions may differ from visual boards in cognitive difficulty
3. **Training Data Contamination**: Chess games and position analyses are abundantly present in training data, which may affect evaluation validity
4. **Score Mapping**: The precise correspondence between Bayesian skill ratings and human FIDE Elo ratings has not been fully validated
5. **Coverage Depth**: Primarily tests middlegame reasoning; coverage of endgames and opening theory is limited

## Data Sources / References

- Google DeepMind Chess Text official release
- Kaggle Leaderboard rating data