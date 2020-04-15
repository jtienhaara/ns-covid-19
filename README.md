# ns-covid-19
Current and historical Nova Scotia COVID-19 stats.

# License
Distributable under Creative Commons Attribution-ShareAlike 4.0 International license:
https://creativecommons.org/licenses/by-sa/4.0/legalcode

# Blather
Because I'm interested in this side of things, and I haven't been able to find anyone else tracking similar stats for Nova Scotia.  Let me know if you have found (or find in future) another source.

Also if any of my math looks wonky to you, please do let me know.

There are * tons * of assumptions (some explicit, and described below; others implicit) in the formulae.  Take all of this with a big ol' grain of salt.

Columns, for anyone who wants to play along at home, with equations given for row 10:

A: Date

B: Confirmed Cases

C: Presumptive Cases

D: Negative

E: Total

F: Rate of Change =(B10+C10)/(B9+C9) - 1 (x100%)

G: Acceleration =(F10+1)/(F9+1) - 1 (x100%)

H: # Doubles =ROUNDDOWN(LOG((B10+C10)/($B$2+$C$2),2))

I: Today's # Days / Doubling=1 / LOG((B10+C10)/(B9+C9),2)

J: Avg # Days / Doubling =COUNT($A$2:A10) / LOG((B10+C10)/($B$2+$C$2),2)

K: # tested today=E10-E9 *NOTE* provincial reports always give a wildly different number, possibly because results are not yet in for those tested in a given day.  The number reported here is the number of tested cases *with results*.

L: # cases recovered

M: # active Cases=B10+C10-L10-N10

N: # deaths

O: 100% of NS population infected, assuming only 20% are known cases (80% undocumented)=923598 * (1 - 0.8)

P: # days until 100% of Nova Scotians are infected (assuming 80% undocumented rate)=LOG(O10,2)*I10

Q: date when 100% of Nova Scotians will be infected, assuming 80% undocumented rate=A10+P10

R: New cases=(B10+C10)-(B9+C9)

S: Estimated active cases: sum of the last 11 rows (including this one) from column R.  This assumes that the average hospital stays is 11 days (at the low end of globally reported averages).

T: # active cases in hospital

U: # hospital cases in ICU (subset of column T)

V: % of active cases in hospital=,T10/S10

...

X: Doubling rate to avoid hospital collapse=playing with numbers until there are no "!"s in column AC.

...

AB: Predictaed # of active cases in hospital, assuming 11 day average stay in hospital, and gradually slowing down the doubling rate to match what's in column X=MAX(0, MIN(O9*0.2,AA9*POWER(2,1/IF(I10=0,2.4,I10))))

AC: Uh-oh an exclamation point appears if the predicted number of active cases in hospital is more than # hospital beds / # respirators / # respiratory therapists.  This is a bit of a wild heuristic, but oh well.==IF(AB10>MIN(AE10,MIN(AF10,AG10)),"!","")


# Sources:

Daily cases: https://novascotia.ca/coronavirus/?fbclid=IwAR37baQpUlEJG7g_mQ6oJh35jotG_H1NUwuWn7yebRgcrDkDJ6N2cQcv8l8#cases

Daily hospital cases: https://twitter.com/nsgov

Backup for both of above (less frequent): http://www.cdha.nshealth.ca/coronavirus

More backup: https://docs.google.com/spreadsheets/d/1D6okqtBS3S2NRC7GFVHzaZ67DuTw7LX49-fqSLwJyeo/edit#gid=942958991

Number of hospital beds in NS: estimated at 273, given 3,142 hospital beds total, and occupancy rate of 91.32%.  See Hospital occupancy rate, below, for details on that estimated calculation.

Number of respirators in NS (240): https://www.cbc.ca/news/canada/nova-scotia/nova-scotia-covid-19-medical-supplies-1.5498682

Respiratory therapists in NS (308): https://www.nscrt.com/images/NSCRT_Annual_Report_2018-2019.pdf

Hospital occupancy rate:
Number of inpatient days / ( # available beds * 365 ) https://www.easycalculation.com/medical/learn-inpatient-occupancy-rate.php
Number of inpatient days 2017-2018 (1,037,410), # beds (3,142): http://www.nshealth.ca/AnnualReport2017-18/numbers.html

Pretty infographic: https://novascotia.ca/coronavirus/data/
