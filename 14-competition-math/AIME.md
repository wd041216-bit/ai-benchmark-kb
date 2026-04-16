# AIME — American Invitational Mathematics Examination Benchmark

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | American Invitational Mathematics Examination |
| Creators | MAA (Mathematical Association of America) |
| Adapted as Benchmark | 2024 |
| Number of Questions | 15 questions/year (AIME 2024), 15 questions/year (AIME 2025) |
| Task Type | Free-response math problems (0-999 integer answers) |
| Dataset Link | https://huggingface.co/datasets (search AIME 2024/2025) |
| Status | ✅ Highly discriminative (top models < 50%) |

## Evaluation Dimensions

AIME is the second-tier competition in the U.S. high school mathematics competition system, significantly more difficult than AMC:

1. **Deep Mathematical Reasoning**: Requires multi-step, creative reasoning
2. **Competition-Level Mathematics**: Covers algebra, number theory, combinatorics, geometry
3. **Precise Calculation**: Answers are integers between 0 and 999
4. **No Multiple Choice**: Pure free-response format

## Example Questions

### AIME 2024 Problem 1
```
Find the number of positive integers less than 1000 that can be expressed as the sum
of consecutive positive integers in exactly two different ways.

Answer: 6
```

### AIME 2025 Problem 8
```
A convex hexagon with area 2025 is inscribed in a circle. The hexagon has exactly
one pair of parallel sides. Find the maximum possible value of the product of the
lengths of the three diagonals of the hexagon that do not share endpoints.

Answer: TBD
```

## Model Performance (April 2026)

| Model | AIME 2024 | AIME 2025 |
|-------|-----------|-----------|
| GPT-5.2 Pro | ~99% | ~97% |
| Gemini 3 Flash Preview | ~97% | ~94% |
| DeepSeek V3.2 Speciale | ~90% | ~89% |
| Claude Opus 4.6 (Thinking) | ~85% | ~80% |
| o3-mini High | ~80% | ~75% |
| DeepSeek R1 | ~79% | ~72% |
| GPT-4 (2023) | ~12% | ~8% |

## Why AIME Is Important

1. **High Discrimination**: Even 2026 frontier models have not reached 100% on AIME 2025
2. **Contamination Resistant**: New questions each year, impossible to have in training data
3. **Mathematical Reasoning Gold Standard**: Tests genuine mathematical reasoning ability
4. **Simple Scoring**: Answers are integers, no ambiguity

## Comparison with Other Math Benchmarks

| Benchmark | Difficulty | Discrimination (2026) | Number of Questions |
|-----------|-----------|----------------------|---------------------|
| GSM8K | Elementary | ⚠️ Saturated | 8,500 |
| MATH | High school-Competition | ⚠️ Approaching saturation | 12,500 |
| AIME 2025 | Competition | ✅ High discrimination | 15 |
| FrontierMath | Research-level | ✅ Extremely high discrimination | ~800 |

## Limitations

1. **Small Number of Questions**: Only 15 questions per year, limited statistical significance
2. **Integer Answers Only**: Does not test proof capabilities
3. **Narrow Coverage**: Does not include university-level mathematics