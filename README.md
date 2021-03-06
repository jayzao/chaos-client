# Chaos

Go client to communicate with Chaos dataset API. 

## Installation:- 

```bash
> GO111MODULE=on go get -u github.com/projectdiscovery/chaos-client/cmd/chaos
```

## Usage:- 

```bash
> chaos -h
```

This will display help for the tool. Here are all the switches it supports.

| Flag    | Description                              | Example                   |
|---------|------------------------------------------|---------------------------|
| -d      | Domain to find subdomains for            | chaos -d uber.com         |
| -count  | Show statistics for the specified domain | chaos -d uber.com -count  |
| -o      | File to write output to (optional)       | chaos -d uber.com -o uber.txt  |
| -f      | File containing subdomains to upload     | chaos -f subdomains.txt   |
| -key    | Chaos key for API                        | chaos -key API_KEY        |
| -silent | Make the output silent                   | chaos -d uber.com -silent |

You can also set the API key as environment variable in your bash profile. 

```bash
export CHAOS_KEY="CHAOS_API_KEY"
```

### How to avail `API_KEY`

As of now Chaos dataset is in beta for testing and API endpoint access available to invited users only, you can request an invite for yourself [here](https://forms.gle/LkHUjoxAiHE6djtU6), we are sending out invites in FIFO manner, so we have no ETA.  

# Running chaos

In order to get subdomains for a domain, use the following command.

```bash
> chaos -d aol.com -silent 
load.on.aol.com
kdc.uas.aol.com
winappsvp.gwinappsvp.ops.aol.com
webmail-a03.webmail.aol.com
qa.cms.aol.com
dpm-lm12.websys.aol.com
games.egslb.aol.com
hotsearches.aol.com
hp.aol.com
hp-desktop.estage.aol.com
prop-w-a-mtc02.evip.aol.com
223e7.ipt.aol.com
hostheader.aol.com
```

NOTE:- 

**Chaos dataset endpoint supports "domain" name as input, "string" or "subdomain" based searches are not supported.**   

To get the number of subdomains without getting actual results, you can use the `count` flag.

```bash
> chaos -d aol.com -count -silent 
10640320
```

Additional subdomains can also be uploaded to the API using the `update` flag. Uploads are limited to 10 MB as of now. The uploaded data will be added to the public dataset and is completely voluntary. 

NOTE:- 

**Only subdomains with valid record gets added to dataset, subdomains with dead records gets eliminated**   


```bash
> cat subs.txt | chaos -update

        __                    
  _____/ /_  ____ _____  _____
 / ___/ __ \/ __  / __ \/ ___/
/ /__/ / / / /_/ / /_/ (__  ) 
\___/_/ /_/\__,_/\____/____/  v1

		projectdiscovery.io

[WRN] Use with caution. You are responsible for your actions
[WRN] Developers assume no liability and are not responsible for any misuse or damage.
[INF] Input processed successfully and subdomains with valid records will be updated to chaos dataset.
```
Subfinder also supports updating data to chaos dataset and can be queried later on the go. 

```bash
> cat domains.txt | subfinder -cd

        __                    
  _____/ /_  ____ _____  _____
 / ___/ __ \/ __  / __ \/ ___/
/ /__/ / / / /_/ / /_/ (__  ) 
\___/_/ /_/\__,_/\____/____/  v1

		projectdiscovery.io

[WRN] Use with caution. You are responsible for your actions
[WRN] Developers assume no liability and are not responsible for any misuse or damage.
[INF] Input processed successfully and subdomains with valid records will be updated to chaos dataset.
```

NOTE: 

**The API is rate-limited to 1 request at time per token (you can issue the next request only when the previous one is finished).**
