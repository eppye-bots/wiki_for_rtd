## Configuration change management (bots\>=3.0)

Having different environments for at least test and production is a sound IT 
practice.  
But having different environments also brings problems:

-   push changes in a controlled way to production-environment
-   are changes done right, and does the existing configuration still
    run right?
-   keep test-environment in line with production-environment
     
To handle these problems bots has some features called
*configuration change management*.


### Bots configuration change management


Configuration change management in bots has 2 aspects:

1.  Use [tools](UsefulTools.md#Compare_and_merge) for:
    -   Comparing differences in configuration of environments
    -   Pushing the changes from test-\>production environment in a
        controlled, automated way

2.  Use of [isolated acceptance test](DeploymentAcceptance.md) to:
    -   check if acceptance test runs OK in test
    -   check if acceptance test runs OK in production
    -   make the test-environment (very) equal to production-environment

Configuration change management works best if both aspects are
combined!

See [receipe](DeploymentAutopush.md) for this!

