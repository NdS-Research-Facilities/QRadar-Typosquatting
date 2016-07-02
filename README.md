# QRadar-Typosquatting
QRadar Custom AQL Property (CAP) determine likely sameness on 2 strings (find Typosquatting)

Can be used to find "almost" matching domain names in email headers in order to detect spearfishing (from: looking like the intended recepient company e.g.)

test_in and test_out are custom properties (extractions from payload) which are the two "to be compared strings"

install with:

/opt/qradar/bin/contentManagement.pl -a update -f eu.ndsrf.cap-fuzzyset.xml


AQL usage sample: 

select "test_in" as ii, "test_out" as oo, NDSRF::ISFUZZY(ii,oo) as ff from events group by ii,oo order by ff desc last 1 DAYS 

Event rule using this test to e.g. create offenses (see fuzzy-rule2.png)

NDSRF::ISFUZZY("test_in","test_out") !=1 AND  NDSRF::ISFUZZY("test_in","test_out") >= 0.1


