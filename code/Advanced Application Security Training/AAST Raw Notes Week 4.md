## Command injection
![[{C381A14B-9A00-48C3-A1A8-19FBF8F280FE}.png]]

![[{C1742159-3C7E-4A9E-AEFB-B510609F5812}.png]]
defending from command injection is relatively simple because of all of the frameworks that get used. ie Oracle java, node, go, etc

there is no need for the application to ever ask the operating system to do anything. Apps talk with the framework, and the framework handles talking to the operating system.

![[{52F487EA-90CB-4258-947B-83EACEA424A4}.png]]

![[{D24C51D9-135B-47F4-8163-212EBE196DB1}.png]]

## Legacy Applications
![[{61AE239F-0BDF-4674-B26A-8ED900DD0024}.png]]  
escape on the command line so the command line passes it as standard text instead of trying to execute the string

![[{843836E5-A804-42EA-9669-F87B8AA9B6AE}.png]]

windows uses a caret symbol  

![[{2DE06754-B6B6-4604-8D24-55B9AC3B9FC2}.png]]

## References
routers are getting hit hard with command injection scripts
usually via the web page at the router page
most of them are out of date
some patch stuff for you, but most vendors are bad about it

![[{D2638926-0785-4154-A92B-CD5B73CED90F}.png]]
## Insecure direct object references
![[{2A7AB67D-63A3-41C9-9EAF-DDECD00359B0}.png]]
![[{F8309EA3-EE73-4606-A59C-8807C6FE60C7}.png]]
![[{D1A083AA-90EB-43B5-9E03-9F78354B006C}.png]]
![[{8E9EA366-A6DB-4C24-AB30-7E118312FF58}.png]]
this can get the vulnerable server to download a remote script from the hacker  and run it !!

![[{3CB9B8E0-E1F3-4440-AA58-8D6C87CC20AB}.png]]
![[{99899C5C-0E79-4446-A920-85EE82689A75}.png]]
![[{B2571093-E693-43E5-B69C-1B8316172EAE}.png]]

> simple-web-shell.command tells you how to do this ?

![[{1C9B6EBC-6C9C-44D3-8884-535F398430B4}.png]]
can confirm the evil code is sitting on the server

now we can pull down the malicious code
![[{D9CBFD88-9265-4913-8CC6-DD7A28D827B4}.png]]

just change the url in the parameter that the server uses

there is an apache server that requests get passed through, so extra parameters need to be encoded.

![[{3B534A3B-F12C-4D5A-ACCF-5F5084E25BE5}.png]]

we now effectively have a command shell  

use lab files that are in the documents directory


![[{84EFDECB-EE58-400C-93CB-29CDCC36FB8F}.png]]

![[{79739013-EBBE-427F-B1A5-346B193B3DF3}.png]]
the user changes the url that is exposed by the front end client
![[{52DED9E0-5B95-4229-91DB-4D519851455A}.png]]
![[{5189DE39-5E37-4806-AD45-614DB52F540B}.png]]
![[{81AEA518-B9F7-4899-BFC3-3695CEE41D10}.png]]

unhide hidden form fields in burpsuite
![[{FE4C8230-16C8-47DE-BCFB-30E51A9B4B44}.png]]

![[{A4933518-1E4B-4BC2-A54E-93A98DAA125D}.png]]
testing for insecure direct object references

a little more difficult for scanners because they are logical issues, such as "how to elevate user to admin", it's not based on a syntax error so it requires more imagination about fraud
![[{A4C47CA0-E2B4-4F9D-8682-49C1D00669A8}.png]]

try to use a static application security testing tool (SAST)

do peer reviews
![[{B616BF27-58D7-4A09-96FA-607C334AC547}.png]]

![[{D5FDF88B-380E-4852-A0D4-0B72AF6D4196}.png]]

jeremy user is the baseline request
doing differential analysis in burpsuite, we can find the request and use it in the intruder tool (add it to the repeater field first)
can use a payload of numbers

payload processing is interesting also and can allow you do things like changing the data and parameters around and such. for instance, highlighting something

![[{BD0A4C5C-2474-40B6-8599-FFB6A4CD9941}.png]]

![[{D2F83DFE-BFA5-4349-B8F8-078257A10EA8}.png]]
![[{568769DF-23CF-4A45-B2A7-54BBC01D46E9}.png]]
For instance, iiq is access control lists

you can let them pick from a meaningless token
![[{01B9CA01-5A7D-472E-9C30-C9DFF8FF05B2}.png]]
dont use a non sequential numbering system
![[{CA2B6BC0-8D39-4E81-98FE-537A283EEAE5}.png]]
![[{2A509CBC-4AFB-4C3A-B61B-A67577B0DE7C}.png]]

## Understanding Open Redirects

![[{82788EF0-6DCD-4575-BC21-7A5325CF69EC}.png]]
![[{ED9A741D-6CCA-4AC8-B84D-AED9488D5BA8}.png]]![[{3D1CE606-7B43-4C1D-BC30-F86FD79733AD}.png]]
![[{E5FE9F54-AF11-4441-A675-D947EA14FE61}.png]]

a hacker will use multiple tricks simultaneously

1- obfuscate the url, a hacker will push everything to the right in the url bar where it's usually not visible to the user unless they go and look.
![[{2779867B-E280-41A0-ACE0-FECD3D2D294A}.png]]
2- obfuscate the parameters of the url. makes the hack more resilient
![[{93691C96-9CD3-407D-A696-CECAAFFDF889}.png]]
![[{275C83EE-07F9-4575-A25C-F4543033BBB4}.png]]

decimal gets converted into an integer encoding
decimal octet notation is for humans

## testing to open redirects
![[{683FE655-D6D0-49A6-B1EA-4D97AD76A036}.png]]
SAST tools are great at this
![[{B8D038B0-778E-4BBC-B601-9790A43AEECF}.png]]

ive seen these in some eud apps

## dynamic analysis testing

manual testing is good for learning and verifying before patching
not good for mass testing/monitoring, etc

![[{010A6BF3-2F3B-4D4F-A03E-036226979186}.png]]
300 and 301 are most important, triggered when redirect caused by the app
![[{E878399D-F99A-4B3C-8AB5-75501C032CCD}.png]]

## preventing open redirects
![[{BA81E219-4CFE-4BDC-95E2-2D53F394732F}.png]]
always use hyperlinks, it might be less convenient, but it's way more secure.
with static redirects, it's hard coded so there is no way to pass parameters

![[{E12CB460-FA24-4821-B05B-C4477C6414B7}.png]]

better when combined with input validation
![[{DB73BCF9-F741-4A05-B93F-9F50238FDD5E}.png]]
