## Samples of mrjob audit usage reports


* Sample report (with one running job flow and one failed-to-start job flow)

```
Total  # of Job Flows: 2

* All times are in UTC.

Min create time: 2015-06-23 16:17:55
Max create time: 2015-06-25 17:18:38
   Current time: 2015-06-25 17:21:39

* All usage is measured in Normalized Instance Hours, which are
  roughly equivalent to running an m1.small instance for an hour.
  Billing is estimated, and may not match Amazon's system exactly.

Total billed:     244.98  100.0%
  Total used:       3.30    1.3%
    bootstrap:      0.13    0.1%
    jobs:           3.17    1.3%
  Total waste:    241.68   98.7%
    at end:         1.25    0.5%
    other:        240.43   98.1%

Daily statistics:

 date          billed      used     waste   % waste
 2015-06-25     86.80      0.95     85.86      98.9
 2015-06-24    120.00      0.00    120.00     100.0
 2015-06-23     38.18      2.35     35.83      93.8

Hourly statistics:

 hour              billed      used     waste   % waste
 2015-06-25 17       1.80      0.39      1.41      78.1
 2015-06-25 16       5.00      0.00      5.00     100.0
 2015-06-25 15       5.00      0.00      5.00     100.0
 2015-06-25 14       5.00      0.00      5.00     100.0
 2015-06-25 13       5.00      0.00      5.00     100.0
 2015-06-25 12       5.00      0.00      5.00     100.0
 2015-06-25 11       5.00      0.00      5.00     100.0
 2015-06-25 10       5.00      0.00      5.00     100.0
 2015-06-25 09       5.00      0.00      5.00     100.0
 2015-06-25 08       5.00      0.00      5.00     100.0
 2015-06-25 07       5.00      0.55      4.45      88.9
 2015-06-25 06       5.00      0.00      5.00     100.0
 2015-06-25 05       5.00      0.00      5.00     100.0
 2015-06-25 04       5.00      0.00      5.00     100.0
 2015-06-25 03       5.00      0.00      5.00     100.0
 2015-06-25 02       5.00      0.00      5.00     100.0
 2015-06-25 01       5.00      0.00      5.00     100.0
 2015-06-25 00       5.00      0.00      5.00     100.0
 2015-06-24 23       5.00      0.00      5.00     100.0
 2015-06-24 22       5.00      0.00      5.00     100.0
 2015-06-24 21       5.00      0.00      5.00     100.0
 2015-06-24 20       5.00      0.00      5.00     100.0
 2015-06-24 19       5.00      0.00      5.00     100.0
 2015-06-24 18       5.00      0.00      5.00     100.0
 2015-06-24 17       5.00      0.00      5.00     100.0
 2015-06-24 16       5.00      0.00      5.00     100.0
 2015-06-24 15       5.00      0.00      5.00     100.0
 2015-06-24 14       5.00      0.00      5.00     100.0
 2015-06-24 13       5.00      0.00      5.00     100.0
 2015-06-24 12       5.00      0.00      5.00     100.0
 2015-06-24 11       5.00      0.00      5.00     100.0
 2015-06-24 10       5.00      0.00      5.00     100.0
 2015-06-24 09       5.00      0.00      5.00     100.0
 2015-06-24 08       5.00      0.00      5.00     100.0
 2015-06-24 07       5.00      0.00      5.00     100.0
 2015-06-24 06       5.00      0.00      5.00     100.0
 2015-06-24 05       5.00      0.00      5.00     100.0
 2015-06-24 04       5.00      0.00      5.00     100.0
 2015-06-24 03       5.00      0.00      5.00     100.0
 2015-06-24 02       5.00      0.00      5.00     100.0
 2015-06-24 01       5.00      0.00      5.00     100.0
 2015-06-24 00       5.00      0.00      5.00     100.0
 2015-06-23 23       5.00      0.00      5.00     100.0
 2015-06-23 22       5.00      0.00      5.00     100.0
 2015-06-23 21       5.00      0.00      5.00     100.0
 2015-06-23 20       5.00      0.00      5.00     100.0
 2015-06-23 19       5.00      0.00      5.00     100.0
 2015-06-23 18       5.00      0.00      5.00     100.0
 2015-06-23 17       5.00      1.13      3.87      77.3
 2015-06-23 16       3.18      1.22      1.96      61.6

* Job flows are considered to belong to the user and job that
  started them or last ran on them.

Top jobs, by total time used:
       1.80 mrjob2
       0.80 user_similarity_jim
       0.55 job
       0.15 mrjob1

Top jobs, by time billed but not used:
     190.53 mrjob2
      48.73 job
       1.87 user_similarity_jim
       0.55 mrjob1

Top users, by total time used:
       3.30 ubuntu

Top users, by time billed but not used:
     241.68 ubuntu

Top job steps, by total time used (step number first):
       0.86   1 mrjob2
       0.81   2 mrjob2
       0.29   2 user_similarity_jim
       0.29   1 job
       0.27   3 user_similarity_jim
       0.27   2 job
       0.24   1 user_similarity_jim
       0.15   1 mrjob1

Top job steps, by total time billed but not used (un-pooled only):
     190.54   2 mrjob2
      48.73   2 job
       1.87   3 user_similarity_jim
       0.55   1 mrjob1
       0.00   1 job
       0.00   1 mrjob2
       0.00   1 user_similarity_jim
       0.00   2 user_similarity_jim

All pools, by total time billed:
     244.98 (not pooled)

All pools, by total time billed but not used:
     241.68 (not pooled)

All job flows, by total time billed:
     244.98 j-3GLYARB78TT46 mrjob2.ubuntu.20150623.161753.123557
       0.00 j-23HR95A13OFRE job.ubuntu.20150625.171840.919349

All job flows, by time billed but not used:
     241.68 j-3GLYARB78TT46 mrjob2.ubuntu.20150623.161753.123557
       0.00 j-23HR95A13OFRE job.ubuntu.20150625.171840.919349

Details for all job flows:

 id              state         created             steps        time ran     billed    waste   user   name
 j-23HR95A13OFRE FAILED        2015-06-25 17:18:38   2           0:00:00      0.00      0.00   ubuntu job
 j-3GLYARB78TT46 WAITING       2015-06-23 16:17:55  23   2 days, 0:59:48      3.30    241.68   ubuntu mrjob2
```

* Right after running `terminate_job_flow`, the tail of the report changes to
```
Details for all job flows:

 id              state         created             steps        time ran     billed    waste   user   name
 j-23HR95A13OFRE FAILED        2015-06-25 17:18:38   2           0:00:00      0.00      0.00   ubuntu job
 j-3GLYARB78TT46 SHUTTING_DOWN 2015-06-23 16:17:55  23   2 days, 1:09:57      3.30    242.53   ubuntu mrjob2
```

* After the job flow is terminated, the tail of the report changes to
```
Details for all job flows:

 id              state         created             steps        time ran     billed    waste   user   name
 j-23HR95A13OFRE FAILED        2015-06-25 17:18:38   2           0:00:00      0.00      0.00   ubuntu job
 j-3GLYARB78TT46 TERMINATED    2015-06-23 16:17:55  23   2 days, 1:10:52      3.30    246.70   ubuntu mrjob2
```
