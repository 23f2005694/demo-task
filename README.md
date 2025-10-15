# Overview
Webhook Tester is a client-only web app to craft, sign, and send webhook requests. It helps you:

- Build requests with custom methods, headers, and payloads
- Optionally sign payloads with HMAC-SHA256 and attach signature/timestamp headers
- Insert helpful placeholders like ${NOW_ISO}, ${UUIDv4}, ${RANDHEX8}
- Preview a ready-to-run cURL command
- Send one or multiple requests with intervals
- Inspect response headers/body and basic timing
- Persist settings in localStorage
- Keep a simple send history (session only)

Note: Browser CORS rules apply. If the target server doesn’t allow cross-origin requests, sending from the browser may fail or not expose the response. In that case, copy and run the provided cURL command in your terminal.

# Setup
No build tools required.

- Option 1: Open index.html in a modern browser.
  - HMAC signing uses Web Crypto, which requires a secure context. If you open the file directly (file://), some browsers may disable it.
- Option 2 (recommended for signing): Serve locally over HTTPS or localhost.
  - For example:
    - Python: python3 -m http.server 5173
    - Node (http-server): npx http-server -p 5173
  - Then navigate to http://localhost:5173

# Usage
1. Enter your webhook URL.
2. Choose method and content type.
3. Edit payload. Use placeholders:
   - ${NOW}, ${NOW_ISO}, ${EPOCH}
   - ${UUIDv4}, ${RAND}, ${RANDHEX8}
4. Add headers as needed. Quick-add chips are provided.
5. Optional signature:
   - Select HMAC-SHA256, set your secret.
   - Configure header name and value template (use ${sig}, and optionally ${ts} if timestamp is enabled).
   - Enable Include timestamp to add a timestamp header (default: X-Signature-Timestamp).
6. Configure concurrent sends and interval if you want multiple requests.
7. Click Send.
8. Inspect:
   - cURL preview (copy if CORS blocks response in-browser).
   - Response headers/body (when available).
   - Status and latency badges.
   - History panel for recent requests.
9. Use Beautify/Minify to format JSON payload. Sample fills a typical user.created event.
10. Reset clears saved settings. Clear response/History for output panels.

Tips:
- If your server doesn’t include CORS headers, use the cURL preview in a terminal on the same network as your server.
- Content-Type is auto-added if not set explicitly in headers.
- application/x-www-form-urlencoded will turn top-level JSON fields into form fields when possible.