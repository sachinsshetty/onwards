SpeedUp-Agent

1. Create test case for main code flow by analyzing code.
2. Verify the test case cover the business code and skip boiler plate code.
3. Measure time of execution with fuzzing data for repeated execution.
4. Refactor part of code which has max time spent,  verify correctness of code. 
5. Measure if code refactor improved speed and also maintained/ reduced complexity of code.
6. Fix any edge cases and security by analyzing OWASP/CVE from similar code
7. All execution on temporary docker containers,
8. Push changes in temopary git branch, after multiple runs are complete, choose the best branch and squash commits to maintain clean timeline.
9. Only push the final branch to forked repo. Do not spam original branch for SLOP avoidance.