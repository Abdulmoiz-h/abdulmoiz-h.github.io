# Reflection — Homework 1: The "Cloud-Native" Resume

## 1. The path of an HTTP request to https://abdulmoiz-h.github.io

1. **URL parsing.** I type `https://abdulmoiz-h.github.io` into Chrome. The browser splits it into the
   scheme (`https`), the host (`abdulmoiz-h.github.io`), and the path (`/`). Because the scheme is
   HTTPS, the default port is 443.
2. **DNS lookup.** The browser has to turn the hostname into an IP address. It checks its own cache,
   then the operating system's cache, then asks a DNS resolver (usually my ISP's or my router's).
   If the resolver doesn't know the answer, it asks a root server, then the `.io` TLD servers, and
   then GitHub's authoritative name servers. Those return the IP addresses of GitHub Pages' servers
   (for example 185.199.108.153), which sit behind GitHub's CDN (Fastly).
3. **TCP connection.** The browser opens a TCP connection to that IP on port 443 using the three-way
   handshake (SYN, SYN-ACK, ACK). The packets travel through my Wi-Fi router, my ISP, and several
   routers across the Internet, and IP routing moves them hop by hop.
4. **TLS handshake.** Because the site uses HTTPS, the browser and server negotiate encryption. The
   server presents a certificate for `*.github.io`, the browser checks that a trusted certificate
   authority signed it, and both sides agree on session keys. From here on, everything is encrypted.
5. **HTTP request.** The browser sends a request like:
   ```
   GET / HTTP/1.1
   Host: abdulmoiz-h.github.io
   User-Agent: Chrome/...
   Accept: text/html
   ```
   The `Host` header matters: thousands of Pages sites share the same IP addresses, and this header is
   how GitHub knows which user's site I want.
6. **Server side.** GitHub Pages maps the host to my repository `abdulmoiz-h.github.io`, finds the
   files it built from the `main` branch, and serves `index.html` for the path `/`. Pages hosts static
   files only, so no server code runs. It just returns the file.
7. **HTTP response.** The server replies with `HTTP/1.1 200 OK`, headers such as
   `Content-Type: text/html; charset=utf-8` and caching headers, and the HTML in the body.
8. **Parsing and more requests.** Chrome parses the HTML and builds the DOM. When it reaches
   `<link rel="stylesheet" href="css/style.css">` and `<img src="assets/profile.svg">`, it sends
   more GET requests over the same connection for those files. After the CSS arrives it builds the
   CSSOM, applies the cascade and specificity rules, lays out the page, and paints it on screen.

## 2. AI Attribution

I used **Claude (Anthropic, Claude Code)** to help build this site.

**Prompt used:** I gave the assignment to Claude and asked "Help me complete this assignment and tell me if im doing anything wrong."

Claude then generated `index.html`, `css/style.css`, the placeholder image in `/assets`, and a draft of
this reflection, using the content from my previous portfolio site. I created the repository and
made all of the commits myself.

**A logic error the AI made that I had to fix manually:**

Claude pulled information from my old website instead of pulling from my current resume and updated experiences, this caused my "Cloud-Native" Resume to be outdated. In order to fix this I had to replace the information with the current experienced on my resume.

For example it put opportunity network on my resume. Although it is a real program that Ive done, it's not relevant to what my career path is. Therefore I had to remove it and replace it with my newer experiences. 
