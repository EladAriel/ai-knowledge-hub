# EVAL-033: Eval: schema and number checks (disposition + citations + numbers)

## Summary

Force every answer into a schema and score it with code. New in the eval rotation on Nov 6.

## Details

Steps (under a day): define Pydantic/instructor schema with disposition, claims[], citations[], numbers[{value,unit,period,source_id}]; 30–50 golden questions with known numbers; trap cases (wrong number, wrong year/period, unsupportable question); schema-miss = hard fail; report six rates (schema fit, valid citations, number accuracy, answered-when-should-decline, declined-when-should-answer, decline handling). Catches confident wrong numbers, wrong year/scale, made-up citations, format drift, answering when should decline.

## Sources

- No external source link (in-house technique note).
