# Fairdrop to Airdrop Calculations 

** The following section describes the Terp DAO token airdrop methodology for stakers and validiators of different chains.** 

The TERP token will be getting airdropped to stakers and validators of various chains through terp-core logic. We are using analytics derived from the hard work by WYND DAO contributors, who went through snapshots of different chains and designed the formulation of reward shares for each stake & validator engaged at various levels with the chains. 

## TEST-NET DAO

The Test Network DAO includes intial proven, trustworthy community members contributing for the good of the project. It will grow as proposals to include members to the DAO will be made, involving those who are depositing CGAS to the treasury, and those postively contributing to the project in various ways.

## CGAS Depositors

The top percentiles of CGAS holders has a HUGE amount of cgas. Those are the real whales. Also, the bottom 20% are essentially, dust accounts, with dozens to 100's of CGAS. 

## Test Net Contributors

There are three ways to have contributed to the test network:

- Infrastructure Maintainers
- Software deployment & contributors
- Positive community engagement

Each contribution method allocates 1/3rd of the airdrops allocation for Test Net Contributors.
Text based proposals within the Test Net DAO will confirm the allocations validity, once we are finalizing the gentx process.

## Forumla: 

We use piecewise linear curves for all items, constant above a minimum and a maximum.

Given user X is percentile /rho in some metric (ie. CGAS deposit amount), we define the reward formula as : 

``` 
Reward(R)= func(p, a, b, min, max)

    =a ; if p < min
    =b ; if p > max 
    =a + ((b-a) * (p-min)/(max-min)) ; otherwise 
``` 

Where a,b are for percentile cutoffs over a range of points in terms of min, max.

We chose the following values for calculating individual reward points for each feature, i.e. CGAS deposit amounts.

```
CGAS deposit points = Reward(p(staked), 20, 80, 0, 100)
``` 


**Positive community engagement** includes anyone who: 
- Communicates effectively with other community members in need 
- Contributes to documentation & other community resources

Contributions can be tracked in discord, & will be confirmed via test net DAO proposal.
