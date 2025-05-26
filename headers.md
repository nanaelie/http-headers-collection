
**HTTP headers** are essential components of HTTP requests and responses. They carry key metadata such as content type, security directives, cache control, origin policies, and more. Proper header configuration improves security, enhances browser compatibility, and protects user privacy.

This collection provides a concise overview of the most useful headers, including:

* their **recommended value**,
* their **effect on browser behavior or security**,
* and the **risks involved** if missing or misconfigured.

# 📦 HTTP Headers

| Header                         | Recommended Value                                               | Effect                                           | Risk                                |
| ------------------------------ | --------------------------------------------------------------- | ------------------------------------------------ | ----------------------------------- |
| `Strict-Transport-Security`    | `max-age=63072000; includeSubDomains; preload`                  | Enforce HTTPS                                    | MITM, downgrade attacks             |
| `Content-Security-Policy`      | `default-src 'self'; script-src 'self' 'unsafe-inline'`         | Prevents XSS and JS injection                    | XSS                                 |
| `X-Frame-Options`              | `DENY` or `SAMEORIGIN`                                          | Prevents clickjacking                            | Clickjacking                        |
| `X-XSS-Protection`             | `1; mode=block`                                                 | Legacy XSS protection                            | Weak protection on old browsers     |
| `X-Content-Type-Options`       | `nosniff`                                                       | Prevents MIME sniffing                           | Execution of malicious content      |
| `Referrer-Policy`              | `strict-origin-when-cross-origin`                               | Controls Referer header                          | Leaks origin URLs                   |
| `Permissions-Policy`           | `geolocation=(), camera=(), microphone=()`                      | Restricts access to sensitive APIs               | Unauthorized access to APIs         |
| `Cross-Origin-Embedder-Policy` | `require-corp`                                                  | Protects against Spectre-type attacks            | JS-based data leaks                 |
| `Cross-Origin-Opener-Policy`   | `same-origin`                                                   | Isolates browsing context                        | Shared execution context            |
| `Cross-Origin-Resource-Policy` | `same-origin`                                                   | Prevents cross-origin resource sharing           | Data leaks                          |
| `Host`                         | `example.com`                                                   | Server routing                                   | Host Header Injection               |
| `User-Agent`                   | `Mozilla/...`                                                   | Client identification                            | Fingerprinting                      |
| `Accept`                       | `text/html,application/json,...`                                | Expected content type                            | Rare                                |
| `Authorization`                | `Bearer <token>` or `Basic <base64>`                            | Authentication                                   | Token leakage                       |
| `Referer`                      | URL of previous page                                            | Navigation tracking                              | Sensitive data leaks                |
| `Origin`                       | `https://client.com`                                            | Cross-origin requests                            | CSRF if unchecked                   |
| `Cookie`                       | `session_id=abc`                                                | Session management                               | XSS if unprotected                  |
| `Content-Type`                 | `application/json`, `multipart/form-data`                       | Body content type                                | Interpretation attacks              |
| `X-Requested-With`             | `XMLHttpRequest`                                                | AJAX request identification                      | CSRF protection                     |
| `Content-Type` (response)      | `text/html`, `application/json`                                 | Response content type                            | MIME sniffing                       |
| `Set-Cookie`                   | `sessionid=abc; HttpOnly; Secure; SameSite=Strict`              | Session cookies                                  | XSS/CSRF if misconfigured           |
| `Cache-Control`                | `no-store`, `max-age=0`                                         | Cache control                                    | Info leaks through cache            |
| `ETag`                         | `W/"xyz"`                                                       | Cache validation                                 | Fingerprinting                      |
| `Location`                     | `/home` or full URL                                             | Redirection control                              | Open redirect attacks               |
| `Access-Control-Allow-Origin`  | `*` or domain                                                   | Cross-origin access                              | Cross-origin data leaks             |
| `Content-Disposition`          | `attachment; filename=...`                                      | File download control                            | Remote code execution (RCE)         |
| `X-Powered-By`                 | (none / remove)                                                 | Technology disclosure                            | Easier fingerprinting               |
| `Server`                       | (none / remove)                                                 | Server version disclosure                        | Version-specific exploits           |
| `Pragma`                       | `no-cache` (deprecated)                                         | Legacy cache control (HTTP/1.0)                  | Unreliable caching                  |
| `X-AspNet-Version`             | (none / remove)                                                 | ASP.NET version disclosure                       | Targeted attacks on known flaws     |
| `Expect-CT`                      | `max-age=86400, enforce, report-uri="..."` | Enforces Certificate Transparency              | Use of misissued TLS certificates   |
| `Feature-Policy` *(obsolete)*    | —                                          | Legacy version of `Permissions-Policy`         | Deprecated, replaced by new header  |
| `Forwarded` / `X-Forwarded-For`  | client IPs                                 | Tracks original client IP (behind proxies)     | IP spoofing if not validated        |
| `Public-Key-Pins` *(deprecated)* | —                                          | Prevents fraudulently issued certificates      | Deprecated due to DoS risk          |
| `Alt-Svc`                        | `h3=":443"; ma=86400`                      | Enables HTTP/3 support                         | Reduced performance without it      |
| `NEL`                            | Valid JSON config                          | Reports network errors to a collector          | No visibility on client-side errors |
| `Report-To`                      | Valid JSON config                          | Defines where to send reports (CSP, NEL, etc.) | No reporting of policy violations   |
| `Connection`                     | `close` or `keep-alive`                    | Manages TCP connection reuse                   | Resource leakage or DoS if abused   |
| `Transfer-Encoding`              | `chunked`                                  | Controls body transfer encoding (streaming)    | Confusion in request parsing        |
| `Upgrade-Insecure-Requests`      | `1`                                        | Requests secure (HTTPS) version of resource    | Mixed content issues                |
| `Content-Language`                  | `en`, `fr`, etc.                                     | Specifies the language of the response                | Wrong localization or indexing issues             |
| `Accept-Language`                   | `en-US,en;q=0.9`                                     | Client preference for language                        | Poor UX if ignored                                |
| `Timing-Allow-Origin`               | `*` or specific origin                               | Controls which origins can access performance metrics | Exposure of timing data to unintended origins     |
| `Early-Data`                        | `1`                                                  | Indicates support for TLS 0-RTT data                  | Replay attacks if not handled properly            |
| `Save-Data` (request)               | `on`                                                 | Client asks for reduced data usage                    | Ignoring may degrade UX for low-bandwidth users   |
| `Device-Memory` (request)           | `<number>` (e.g., 8)                                 | Hints about client device memory                      | Can be used for adaptive performance              |
| `Viewport-Width` (request)          | `<number>` (e.g., 360)                               | Informs the server of viewport size                   | UX mismatch if ignored                            |
| `DNT`                               | `1`                                                  | Do Not Track user preference                          | Ignoring it can violate privacy expectations      |
| `Accept-CH`                         | `Device-Memory, Viewport-Width, DPR, RTT`            | Instructs client to send specific Client Hints        | Limited device-adaptive delivery if missing       |
| `X-DNS-Prefetch-Control`            | `on` or `off`                                        | Controls DNS prefetching                              | DNS leaks or delay if misused                     |
| `X-Permitted-Cross-Domain-Policies` | `none`                                               | Restricts Flash/Silverlight cross-domain policies     | Legacy RIA attacks if misconfigured               |
| `Clear-Site-Data`                   | `"cache", "cookies", "storage", "executionContexts"` | Clears site data on logout or after sensitive actions | Residual data remains if not cleared              |
| `Service-Worker-Allowed`            | `/` or limited scope                                 | Defines the allowed scope for service workers         | Unintended scope takeover                         |
| `Sec-Fetch-Site`                    | `same-origin`, `same-site`, `cross-site`             | Part of Fetch Metadata Request Headers                | CSRF/XSSI protection when validated properly      |
| `Sec-Fetch-Mode`                    | `navigate`, `cors`, etc.                             | Indicates how the request will be used                | Abuse of unexpected modes                         |
| `Sec-Fetch-Dest`                    | `document`, `script`, `image`, etc.                  | Indicates destination context of request              | Misclassification or security bypass              |
| `Sec-Fetch-User`                    | `?1` (sent only if initiated by user interaction)    | Helps identify user-initiated requests                | Automated attacks may bypass if not checked       |
| `Accept-Encoding`                   | `gzip, br`                                           | Tells server accepted compression methods             | Inefficient responses if not supported            |
| `Content-Encoding`                  | `gzip`, `br`, `deflate`                              | Indicates how response body is compressed             | Decompression attacks if misused (e.g., zip bomb) |

---
