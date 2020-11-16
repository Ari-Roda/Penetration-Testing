
1. Initial Reconaisonce begins by understanding engagement requirements deeply. There can be lots of crucial information within the engagement document.

2. Check open sources on target.

  2a. Checking targets actual website.
      2aa. Chicking Organization structure, board of directors profiles, executive profiles, products, job vacancies, partners, suppliers, employees from blog.
  2b. Check social media of target.
      2ba. Find target company employees  
            -Facebook, Twitter, Linkedin, Google+ etc (social network can depend on target compnies industry and interest eg. if target company is in media or advertisement Instagram might be best. Also specific niche social networks/forums and messageboards for targets industry can be useful)
            - Some SNS sites allow for account linking, eg Twitter to Facebook etc. Can leverage this to find more information on target. Linkedin Forces users to use real name so if can find connection to linkedin account, from twitter or other SNS can get good PII.

3. Whois database and other sites can be used to find further detailed information. 

4. Find example emails and try to determine the email schema they might use internally. You may get this from the site itself, Social media like linkedin or other site, or you might have to email someone internally and check their email. If none of these work you can try to guess the email schema using common ones such as name.surname@company.com, surname.name@company.com, first letter of namesurname@company.com. You can then send to employees found through SNS in this format, if the email doesnt exist you should get a email in return saying so but not always. The email you send shouldnt be suspicious and alert anyone, so make it look like spam possibly. Check the emails that didnt get sent to know the correct email schema.

5.Find as many websites owned by the company as possible. Enumerating the main domain may find various subdomains available that contain valuable information. At this stage passive enumeration should be used meaning we do not directly interact with the target. Instead we can use google and other online resources to search for available domains owned by the company. In Google you can use site: company.com to search based on particular domain. Also dnsdumpster.com indexes search sites for information. Sublist3r collects DNS data from various sources. Virustotal lists many of these things in one place also by searching for the domain in question. Crt.sh allows you to search certificates for a site where you can find valid subdomains from them. This can also be done by viewing the certificate of a site through the browser, going to details and certificate subject alternative name. Which can show all subdomains covered by that certificate. Sublister has a built in brute force option which uses a domain list to brute force common subdomain names called names.txt. You can use this one or try another one like dirbuster etc. Be careful that some subdomains will just redirect to the main page and therefore some scans will show it as up when its not of any use to us. amass is another dns enumeration and network mapping tool. snap run amass -ip -d google.com. bruteforicing subdomains takes time so start with passive methods
        
As you find new sources you repeat the same processes in a cycle manner to not miss anything.

###################################################################################################################

6. Google dorks : google dorks can be used to find specific resources that are publicly available.

inurl:admin intitle:login site:example.com

this can be linked with AND/OR/& to make it more specific.


intext:credentials -inurl: (htm|html|php|asp|jsp) intitle:"index of" "last modified" "parent directory" txt OR doc OR pdf site:.jp

minus can be used to exclude commom extensions, and look for open directory indexes containing a string and txt doc or pdf file in certain tld
