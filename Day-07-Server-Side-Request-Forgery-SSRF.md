# Day 07 - SSRF (Server-Side Request Forgery)

## What It Is
SSRF is a web attack where an attacker tricks a server into making HTTP requests to an unintended location — either internal network resources or external systems. Instead of the attacker's browser making the request directly, the vulnerable server makes it on their behalf. This lets attackers reach internal systems that are normally completely hidden from the outside world.

## How It Works
Many web apps fetch remote resources based on user input — things like URL previews, image fetchers, PDF generators, or webhook validators. If the app doesn't validate what URLs it's allowed to fetch, an attacker can point it at internal infrastructure instead.

Simple example - an image fetcher feature:
```
# Normal usage
https://app.com/fetch?url=https://example.com/image.jpg

# SSRF attack - attacker points it at internal metadata service
https://app.com/fetch?url=http://169.254.169.254/latest/meta-data/

# Or internal services not exposed to the internet
https://app.com/fetch?url=http://localhost:8080/admin
https://app.com/fetch?url=http://192.168.1.1/internal-api
```

The server fetches the URL and returns the response. From the server's perspective it's just making an internal request — totally allowed. The attacker now gets data from internal systems they should never have access to.
