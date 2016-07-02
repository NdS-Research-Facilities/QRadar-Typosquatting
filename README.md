# QRadar-Typosquatting
QRadar Custom AQL Property (CAP) determine likely sameness on 2 strings (find Typosquatting)

Can be used to find "almost" matching domain names in email headers in order to detect spearfishing (from: looking like the intended recepient company e.g.)

install with:

/opt/qradar/bin/contentManagement.pl -a update -f eu.ndsrf.cap-fuzzyset.xml


AQL usage sample: 
select "test_in" as ii, "test_out" as oo, NDSRF::ISFUZZY(ii,oo) as ff from events group by ii,oo order by ff desc last 1 DAYS 

