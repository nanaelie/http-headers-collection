
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

