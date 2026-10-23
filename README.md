# k6-lab
- Step 0.1, http_req_duration: avg=317.06ms, p(95)=317.06ms
- Step 0.2: 73 requests, 3.51219 req/s, p(95) = 347.77 ms.
  The rate was below 5 req/s because each iteration included the HTTP
  response time and a one-second sleep.
- Step 0.3: iteration_duration: avg=1.53s, p(95)=2.05s
- Step 0.4: status is 200, pizza has a name, every ingredient is vegetarian