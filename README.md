# K6 lab results

## Part 0

- Step 0.1, `http_req_duration`: avg = 317.06 ms, p(95) = 317.06 ms.
- Step 0.2: 73 requests, 3.51219 req/s, and p(95) = 347.77 ms. The request rate stayed below 5 req/s because each iteration included both the HTTP response time and a one-second sleep.
- Step 0.3: `iteration_duration`: avg = 1.53 s, p(95) = 2.05 s.
- Step 0.4: All checks passed: `status is 200`, `pizza has a name`, and `every ingredient is vegetarian`.
- Step 0.5: The `request without a token is refused` check passed, and `http_req_failed` was 0.00%.
- Step 0.6: The normal run returned exit code 0. The run with `P95=300` failed the response-time threshold and returned exit code 99.
- Step 0.7: The `http_req_failed` rule passed with a failure rate of 0.00%. The response-time rules failed: p(95) = 1.24 s, which exceeded 1 second, and p(99) = 1.59 s, which exceeded 1.5 seconds. The test returned exit code 99.
- Step 0.8: The `no pepperoni` and `no knife needed` checks initially failed. The request used lowercase `pepperoni` and `knife`, but the API values were case-sensitive and used `Pepperoni` and `Knife`. Therefore, the exclusions were not applied correctly. Repeated requests under load generated different random pizza recommendations, making the defect easier to detect than with a single manual request. After correcting the capitalization, all checks passed.

## Part A results

| Step | Test type | Users | Req/s | p(95) | Max | Failed | Checks |
| ---- | --------- | ----: | ----: | -----: | --: | -----: | -----: |
| A1 | Smoke | 1 | 0.493402/s | 359.93 ms | 383.71 ms | 0.00% | 100.00% |
| A2 | Average load | 3 | 1.30987/s | 381.44 ms | 391.16 ms | 0.00% | 100.00% |
| A3 | Stress | 5 | 2.17768/s | 382.82 ms | 411.36 ms | 0.00% | 100.00% |
| A4 | Spike | 5 | 1.048961/s | 385.86 ms | 404.99 ms | 0.00% | 100.00% |
| A5 | Soak | 2 | 0.977977/s | 378.06 ms | 417.32 ms | 0.00% | 100.00% |

Notes:

- A1 completed 5 iterations and 15 HTTP requests. The average response time was 305.83 ms, and p(95) was 359.93 ms.
- A2 completed 80 iterations and 240 HTTP requests. The average response time was 297.45 ms, and p(95) was 381.44 ms. All thresholds passed.
- A3 completed 134 iterations and 402 HTTP requests. The average response time was 300.32 ms, and p(95) was 382.82 ms. This was 1.38 ms higher than A2. All thresholds passed.
- A4 completed 49 iterations and 147 HTTP requests. The average response time was 302.39 ms, and p(95) was 385.86 ms. The response time increased during the spike. After the load returned to 1 VU, it took approximately 60 seconds to return to its earlier level.
- A5 completed 216 iterations and 648 HTTP requests. The average response time was 296.39 ms, and p(95) was 378.06 ms. All 864 checks passed, and all thresholds passed.