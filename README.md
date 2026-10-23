# k6-lab
- Step 0.1, http_req_duration: avg=317.06ms, p(95)=317.06ms
- Step 0.2: 73 requests, 3.51219 req/s, p(95) = 347.77 ms.
  The rate was below 5 req/s because each iteration included the HTTP
  response time and a one-second sleep.
- Step 0.3: iteration_duration: avg=1.53s, p(95)=2.05s
- Step 0.4: ✓ status is 200, ✓ pizza has a name, ✓ every ingredient is vegetarian
- Step 0.5: request without a token is refused, http_req_failed 0.00%
- Step 0.6: Exit code = 0, Exit code = 99
- Step 0.7: ✗ p(95)=1.24s, ✗ p(99)=1.59s, ✓ rate=0.00%, Exit code = 99k6 run explore.js
- Step 0.8: ✗ no pepperoni, ✗ no knife needed; The request used lowercase pepperoni and knife, but the API’s known values were case-sensitive and used Pepperoni and Knife. Therefore, the exclusions were not applied correctly. Repeated requests under load generated multiple random pizza recommendations, making the defect easier to detect than a single manual request.