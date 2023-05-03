# WaPen Methodology

### WaPen Steps
1) Map your application with manual browsing + passive scanning enabled
2) Scan all application pages that accept parameters with Burp (look for the `Params` checkmark in the **target** tab)
	- Scan `GET` requests
	- Scanning `POST`s is dangerous. Best not to do ever? Address this later
	- Right click on hostname on sitemap --> `Actively scan this host` is **NOT** recommended
3) Perform manual fuzzing on against parameters in requests that seem interesting


## Launch a Scan
- Crawl+Audit = **Will send attack traffic and crawl the site!** Automatically sends requets to the server.
- Passive = Looks for security vulnerabilities inside of your requests/responses you've already sent/recieved. This is a passive action, no new requests are made to the server.
- Content Discovery Tool - used for UNAUTHENTICATED DISCOVERY
Within Burp Suite, use the Content Discovery tool to automatically map the application.
	- Open Burp to Target -> Site Map.
	- Right click on the top level site.
	- Select Engagement tools -> Discover content.
	- Examine if new content is discovered.

## Fuzz everything
- PayloadAllTheThings
- Burp Pro has proprietary lists

## Inspect Everything

# Nessus Scan
- Perform a nessus scan with the `NetSPI Standard` config


## How to Record a Micro (auth)
How to record `micro` (auth) for crawl and audit:
	- New Scan --> Application login
	- `Use recorded login sequences`
	- Then go to **Proxy** --> Intercept --> Open browser
	- Using the Burp chrome extension, go-to `Navigation Recorder` --> New recording
	- Log-in to the app, and click on some stuff that you would need to be authenticated to to access
	- When done, hit done recording
	- Your clipboard now has information about your logged-in session
	- Go back to `Application login` --> Use recorded login sequences and paste your clipboard
	- Hit OK and start your authenticated scan!
  
## Autorize
