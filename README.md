# Axiom_Workflow
### First generate subdomains locally or use axiom to hostnames.txt

axiom-fleet BASE_NAME -i NUMBER_TO_SPIN

axiom-select 'BASE_NAME*'

axiom-scan hostnames.txt -m httpx | tee alive.txt

axiom-scan alive.txt -m gau | tee gau.out

cat gau.txt | grep -aiE '^http' | grep -aiE '\?' | qsreplace FUZZ > fuzzable_urls.txt

cat fuzzable_urls.txt | grep FUZZ | gf xss | grep -iavE 'pdf|txt|\?l=FUZZ$|\?contry=FUZZ$|\?q=FUZZ$|is/image' > filtered_fuzzable_urls.txt


axiom-scan filtered_fuzzable_urls.txt -m dalfox | tee dalfox_output.txt


When finished

axiom-rm 'BASE-NAME*'

(Forget this step, and it's instant poverty!)


