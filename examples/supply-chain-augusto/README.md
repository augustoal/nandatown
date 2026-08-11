# Supply-chain experiment

## Choice

I chose the `supply_chain` scenario because it models a chain with different sequential steps where one error can increase exponentially.

The base scenario processes 5 rounds with 3 items per round, for 15 items in total. It is useful for testing whether messages survive several sequential steps.

## Hypothesis

The baseline uses `failures.message_drop: 0.0`. In `my.yaml`, I changed it to 0.01. I wanted to change it really little because I think that a small change here can have greater effects downstream, as each step requires the previous one.

## Results

| Run | Message drop | Messages | Dropped | Delivery / success |
|---|---:|---:|---:|---:|
| Baseline | 0.00 | 120 | 0 | 100.00% |
| `my.yaml` | 0.01 | 112 | 2 | 96.49% |

The saved evidence is in [`evidence/`](evidence/):

- [`baseline.jsonl`](evidence/baseline.jsonl) and [`baseline-report.html`](evidence/baseline-report.html)
- [`edited.jsonl`](evidence/edited.jsonl) and [`edited-report.html`](evidence/edited-report.html)

## Investigation
The results show 96.49% of delivery success, but that is not a completely accurate picture. Because some messages were dropped, a lot less messages were sent: instead of 120, there were 112. If the messages are lost in the first part of the chain, then this is even worse, because less messages get sent after. 
I think it shows that a small percent of failure can add a lot of problems and the importance of >99.99% accuracy in some fields.
In this case the messages were lost in manufacturer->distributor and distributor->retailer. I checked that in the html report, comparing what each agent sent and what each one received.

## Use of AI

I used OpenAI Codex to help me set up the Python environment, inspect the repository structure, copy and format the results in this readme and lastly to create a diagram showing the messages movement in the chain. I personally ran the tests, reviewed the configuration and results and wrote this readme.
