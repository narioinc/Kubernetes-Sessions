# To run scale test on your httpbin service

Expose httbin service to your local

``` $ kubectl port-forward svc/httpbin 8001:8000 ``` 

Here, 8000 is the port of the kubernetes servcie and 8001 is your localhost port where you are proxying the request

Once this is done 

Open the httpbin-scale.js file and change the port on line 5 to what you have given as the locahost port above

# Install K6

Install k6 in your system using the link below:
https://k6.io/docs/get-started/installation/

All major OSes are supported.

# Run the load tester.

You are all set, cd to this directory and run the command below

``` $ k6 run --vus 10 --duration 30s httpbin-scale.js ```

This tells k6 to create 10 virtual users (vus) and run the test written in httpbin-scale.js for 30 seconds

You should see a output like below:

```
k6 run --vus 10 --duration 30s httpbin-scale.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: httpbin-scale.js
     output: -

  scenarios: (100.00%) 1 scenario, 10 max VUs, 1m0s max duration (incl. graceful stop):
           * default: 10 looping VUs for 30s (gracefulStop: 30s)


running (0m30.0s), 00/10 VUs, 26922 complete and 0 interrupted iterations
default ✓ [======================================] 10 VUs  30s

     data_received..................: 265 MB 8.8 MB/s
     data_sent......................: 2.2 MB 72 kB/s
     http_req_blocked...............: avg=5.52µs  min=0s     med=0s      max=9.99ms  p(90)=0s      p(95)=0s
     http_req_connecting............: avg=371ns   min=0s     med=0s      max=1ms     p(90)=0s      p(95)=0s
     http_req_duration..............: avg=11.08ms min=1.99ms med=10.78ms max=67.88ms p(90)=13.27ms p(95)=14.8ms
       { expected_response:true }...: avg=11.08ms min=1.99ms med=10.78ms max=67.88ms p(90)=13.27ms p(95)=14.8ms
     http_req_failed................: 0.00%  ✓ 0          ✗ 26922
     http_req_receiving.............: avg=67.94µs min=0s     med=0s      max=10.41ms p(90)=505.8µs p(95)=526.5µs
     http_req_sending...............: avg=9.56µs  min=0s     med=0s      max=1ms     p(90)=0s      p(95)=0s
     http_req_tls_handshaking.......: avg=0s      min=0s     med=0s      max=0s      p(90)=0s      p(95)=0s
     http_req_waiting...............: avg=11ms    min=1.99ms med=10.64ms max=67.87ms p(90)=13.2ms  p(95)=14.7ms
     http_reqs......................: 26922  896.985623/s
     iteration_duration.............: avg=11.13ms min=1.99ms med=10.92ms max=77.88ms p(90)=13.31ms p(95)=14.87ms
     iterations.....................: 26922  896.985623/s
     vus............................: 10     min=10       max=10
     vus_max........................: 10     min=10       max=10


```

Some of the important aspects of this tool are

* it can tell you you http failures from the  http_req_failed attributes
* it can tell you the breakdown of the different network gates during the HTTP call enabling you to figure out where in the network chain your latency issues are
* it can tell you data recieved and data sent to calcualte your network costs in the cloud and optimize them