# QRadar-Typosquatting
QRadar Custom AQL Function (CAF) determine likely sameness on 2 strings (find Typosquatting ) see https://www.proofpoint.com/us/threat-insight/post/Attackers-Increasing-Use-Of-Typosquatting

Can be used to find "almost" matching domain names in email headers in order to detect spearfishing (from: looking like the intended recepient company e.g.)


Install eu.ndsrf.qradar-typosquatting.zip through Admin > Extension Management


test_in and test_out are custom properties (extractions from payload) which are the two "to be compared strings"

AQL usage sample: 

select "test_in" as ii, "test_out" as oo, NDSRF::ISFUZZY(ii,oo) as ff from events group by ii,oo order by ff desc last 1 DAYS 

Event rule can be using this test to e.g. create offenses (see fuzzy-rule2.png)
Example below will create an offense when the two names are not the same (!=1) and above a non-match (which you will need to tuned in your environment)


NDSRF::ISFUZZY("test_in","test_out") !=1 AND  NDSRF::ISFUZZY("test_in","test_out") >= 0.1


