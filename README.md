# Redlib

> An alternative private front-end to Reddit

# ⚠️ Why do I get TOO MANY REQUESTS errors? ⚠️
#### As of July 12th, 2023, Redlib is currently not operational as Reddit's API changes, that were designed to kill third-party apps and content scrapers who don't pay [large fees](https://www.theverge.com/2023/5/31/23743993/reddit-apollo-client-api-cost), went into effect. [Read the full announcement here.](https://github.com/libreddit/libreddit/issues/840)

![screenshot](https://i.ibb.co/QYbqTQt/libreddit-rust.png)

---

**10-second pitch:** Redlib is a private front-end like [Invidious](https://github.com/iv-org/invidious) but for Reddit. Browse the coldest takes of [r/unpopularopinion](https://libreddit.spike.codes/r/unpopularopinion) without being [tracked](#reddit).

- 🚀 Fast: written in Rust for blazing-fast speeds and memory safety
- ☁️ Light: no JavaScript, no ads, no tracking, no bloat
- 🕵 Private: all requests are proxied through the server, including media
- 🔒 Secure: strong [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) prevents browser requests to Reddit

---

I appreciate any donations! Your support allows me to continue developing Redlib.

<a href="https://www.buymeacoffee.com/spikecodes" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 40px" ></a>
<a href="https://liberapay.com/spike/donate"><img alt="Donate using Liberapay" src="https://liberapay.com/assets/widgets/donate.svg" style="height: 40px"></a>


**Bitcoin:** `bc1qwyxjnafpu3gypcpgs025cw9wa7ryudtecmwa6y`

**Monero:** `45FJrEuFPtG2o7QZz2Nps77TbHD4sPqxViwbdyV9A6ktfHiWs47UngG5zXPcLoDXAc8taeuBgeNjfeprwgeXYXhN3C9tVSR`

---

# Instances

🔗 **Want to automatically redirect Reddit links to Redlib? Use [LibRedirect](https://github.com/libredirect/libredirect) or [Privacy Redirect](https://github.com/SimonBrazell/privacy-redirect)!**

[Follow this link](https://github.com/libreddit/libreddit-instances/blob/master/instances.md) for an up-to-date table of instances in Markdown format. This list is also available as [a machine-readable JSON](https://github.com/libreddit/libreddit-instances/blob/master/instances.json).

Both files are part of the [libreddit-instances](https://github.com/libreddit/libreddit-instances) repository. To contribute your [self-hosted instance](#deployment) to the list, see the [libreddit-instances README](https://github.com/libreddit/libreddit-instances/blob/master/README.md).

---

# About

Find Redlib on 💬 [Matrix](https://matrix.to/#/#redlib:matrix.org), 🐋 [Quay.io](https://quay.io/repository/redlib/redlib), :octocat: [GitHub](https://github.com/redlib-org/redlib), and 🦊 [GitLab](https://gitlab.com/redlib/redlib).

## Built with

- [Rust](https://www.rust-lang.org/) - Programming language
- [Hyper](https://github.com/hyperium/hyper) - HTTP server and client
- [Askama](https://github.com/djc/askama) - Templating engine
- [Rustls](https://github.com/rustls/rustls) - TLS library

## Info
Redlib hopes to provide an easier way to browse Reddit, without the ads, trackers, and bloat. Redlib was inspired by other alternative front-ends to popular services such as [Invidious](https://github.com/iv-org/invidious) for YouTube, [Nitter](https://github.com/zedeus/nitter) for Twitter, and [Bibliogram](https://sr.ht/~cadence/bibliogram/) for Instagram.

Redlib currently implements most of Reddit's (signed-out) functionalities but still lacks [a few features](https://github.com/libreddit/libreddit/issues).

## How does it compare to Teddit?

Teddit is another awesome open source project designed to provide an alternative frontend to Reddit. There is no connection between the two, and you're welcome to use whichever one you favor. Competition fosters innovation and Teddit's release has motivated me to build Redlib into an even more polished product.

If you are looking to compare, the biggest differences I have noticed are:
- Redlib is themed around Reddit's redesign whereas Teddit appears to stick much closer to Reddit's old design. This may suit some users better as design is always subjective.
- Redlib is written in [Rust](https://www.rust-lang.org) for speed and memory safety. It uses [Hyper](https://hyper.rs), a speedy and lightweight HTTP server/client implementation.

---

# Comparison

This section outlines how Redlib compares to Reddit.

## Speed

Lasted tested Nov 11, 2022.

Results from Google PageSpeed Insights ([Redlib Report](https://pagespeed.web.dev/report?url=https%3A%2F%2Flibreddit.spike.codes%2F), [Reddit Report](https://pagespeed.web.dev/report?url=https://www.reddit.com)).

|                        | Redlib   | Reddit    |
|------------------------|-------------|-----------|
| Requests               | 60          | 83        |
| Speed Index            | 2.0s        | 10.4s     |
| Time to Interactive    | **2.8s**    | **12.4s** |

## Privacy

### Reddit

**Logging:** According to Reddit's [privacy policy](https://www.redditinc.com/policies/privacy-policy), they "may [automatically] log information" including:
- IP address
- User-agent string
- Browser type
- Operating system
- Referral URLs
- Device information (e.g., device IDs)
- Device settings
- Pages visited
- Links clicked
- The requested URL
- Search terms

**Location:** The same privacy policy goes on to describe that location data may be collected through the use of:
- GPS (consensual)
- Bluetooth (consensual)
- Content associated with a location (consensual)
- Your IP Address

**Cookies:** Reddit's [cookie notice](https://www.redditinc.com/policies/cookies) documents the array of cookies used by Reddit including/regarding:
- Authentication
- Functionality
- Analytics and Performance
- Advertising
- Third-Party Cookies
- Third-Party Site

### Redlib

For transparency, I hope to describe all the ways Redlib handles user privacy.

#### Server

* **Logging:** In production (when running the binary, hosting with docker, or using the official instances), Redlib logs nothing. When debugging (running from source without `--release`), Redlib logs post IDs fetched to aid with troubleshooting.

* **Cookies:** Redlib uses optional cookies to store any configured settings in [the settings menu](https://libreddit.spike.codes/settings). These are not cross-site cookies and the cookies hold no personal data.

#### Official instance (libreddit.spike.codes)

The official instance is hosted at https://libreddit.spike.codes.

* **Server:** The official instance runs a production binary, and thus logs nothing.

* **DNS:** The domain for the official instance uses Cloudflare as the DNS resolver. However, this site is not proxied through Cloudflare, and thus Cloudflare doesn't have access to user traffic.

* **Hosting:** The official instance is hosted on [Replit](https://replit.com/), which monitors usage to prevent abuse. I can understand if this invalidates certain users' threat models, and therefore, self-hosting, using unofficial instances, and browsing through Tor are welcomed.

---

# Installation

## 1) Cargo

Make sure Rust stable is installed along with `cargo`, Rust's package manager.

```
cargo install libreddit
```

## 2) Docker

Deploy the [Docker image](https://quay.io/repository/redlib/redlib) of Redlib:
```
docker pull quay.io/redlib/redlib
docker run -d --name redlib -p 8080:8080 quay.io/redlib/redlib
```

Deploy using a different port (in this case, port 80):
```
docker pull quay.io/redlib/redlib
docker run -d --name redlib -p 80:8080 quay.io/redlib/redlib
```

To deploy on `arm64` platforms, simply replace `quay.io/redlib/redlib` in the commands above with `quay.io/redlib/redlib:arm`.

To deploy on `armv7` platforms, simply replace `quay.io/redlib/redlib` in the commands above with `quay.io/redlib/redlib:armv7`.

## 3) AUR

For ArchLinux users, Redlib is available from the AUR as [`libreddit-git`](https://aur.archlinux.org/packages/libreddit-git).

```
yay -S libreddit-git
```
## 4) NetBSD/pkgsrc

For NetBSD users, Redlib is available from the official repositories.

```
pkgin install libreddit
```

Or, if you prefer to build from source

```
cd /usr/pkgsrc/libreddit
make install
```

## 5) GitHub Releases

If you're on Linux and none of these methods work for you, you can grab a Linux binary from [the newest release](https://github.com/redlib-org/redlib/releases/latest).

## 6) Replit/Heroku/Glitch

> **Warning**
> These are free hosting options, but they are *not* private and will monitor server usage to prevent abuse. If you need a free and easy setup, this method may work best for you.

<a href="https://repl.it/github/redlib-org/redlib"><img src="https://repl.it/badge/github/redlib-org/redlib" alt="Run on Repl.it" height="32" /></a>
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/redlib-org/redlib)
[![Remix on Glitch](https://cdn.glitch.com/2703baf2-b643-4da7-ab91-7ee2a2d00b5b%2Fremix-button-v2.svg)](https://glitch.com/edit/#!/remix/libreddit)

---

# Deployment

Once installed, deploy Redlib to `0.0.0.0:8080` by running:

```
redlib
```

## Instance settings

Assign a default value for each instance-specific setting by passing environment variables to Redlib in the format `REDLIB_{X}`. Replace `{X}` with the setting name (see list below) in capital letters.

| Name                      | Possible values | Default value    | Description                                                                                               |
|---------------------------|-----------------|------------------|-----------------------------------------------------------------------------------------------------------|
| `SFW_ONLY`                | `["on", "off"]` | `off`            | Enables SFW-only mode for the instance, i.e. all NSFW content is filtered.                                |
| `BANNER`                  | String          | (empty)          | Allows the server to set a banner to be displayed. Currently this is displayed on the instance info page. | 
| `ROBOTS_DISABLE_INDEXING` | `["on", "off"]` | `off`            | Disables indexing of the instance by search engines.                                                      |
| `PUSHSHIFT_FRONTEND`      | String          | `www.unddit.com` | Allows the server to set the Pushshift frontend to be used with "removed" links.                          |

## Default User Settings

Assign a default value for each user-modifiable setting by passing environment variables to Redlib in the format `REDLIB_DEFAULT_{Y}`. Replace `{Y}` with the setting name (see list below) in capital letters.

| Name                                | Possible values                                                                                                                    | Default value |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|---------------|
| `THEME`                             | `["system", "light", "dark", "black", "dracula", "nord", "laserwave", "violet", "gold", "rosebox", "gruvboxdark", "gruvboxlight"]` | `system`      |
| `FRONT_PAGE`                        | `["default", "popular", "all"]`                                                                                                    | `default`     |
| `LAYOUT`                            | `["card", "clean", "compact"]`                                                                                                     | `card`        |
| `WIDE`                              | `["on", "off"]`                                                                                                                    | `off`         |
| `POST_SORT`                         | `["hot", "new", "top", "rising", "controversial"]`                                                                                 | `hot`         |
| `COMMENT_SORT`                      | `["confidence", "top", "new", "controversial", "old"]`                                                                             | `confidence`  |
| `SHOW_NSFW`                         | `["on", "off"]`                                                                                                                    | `off`         |
| `BLUR_NSFW`                         | `["on", "off"]`                                                                                                                    | `off`         |
| `USE_HLS`                           | `["on", "off"]`                                                                                                                    | `off`         |
| `HIDE_HLS_NOTIFICATION`             | `["on", "off"]`                                                                                                                    | `off`         |
| `AUTOPLAY_VIDEOS`                   | `["on", "off"]`                                                                                                                    | `off`         |
| `SUBSCRIPTIONS`                     | `+`-delimited list of subreddits (`sub1+sub2+sub3+...`)                                                                            | _(none)_      | 
| `HIDE_AWARDS`                       | `["on", "off"]`                                                                                                                    | `off`         |
| `DISABLE_VISIT_REDDIT_CONFIRMATION` | `["on", "off"]`                                                                                                                    | `off`         |
| `DISABLE_STATS_COLLECTION`          |  Any string to disable                                                                                                             | _(none)_      |
| `HIDE_SCORE`                        | `["on", "off"]`                                                                                                                    | `off`         |
| `FIXED_NAVBAR`                      | `["on", "off"]`                                                                                                                    | `on`          |

You can also configure Redlib with a configuration file. An example `redlib.toml` can be found below:

```toml
REDLIB_DEFAULT_WIDE = "on"
REDLIB_DEFAULT_USE_HLS = "on"
```

### Examples

```bash
REDLIB_DEFAULT_SHOW_NSFW=on redlib
```

```bash
REDLIB_DEFAULT_WIDE=on REDLIB_DEFAULT_THEME=dark redlib -r
```

## Proxying using NGINX

> **Note**
> If you're [proxying Redlib through an NGINX Reverse Proxy](https://github.com/libreddit/libreddit/issues/122#issuecomment-782226853), add
> ```nginx
> proxy_http_version 1.1;
> ```
> to your NGINX configuration file above your `proxy_pass` line.

## systemd

You can use the systemd service available in `contrib/redlib.service`
(install it on `/etc/systemd/system/redlib.service`).

That service can be optionally configured in terms of environment variables by
creating a file in `/etc/redlib.conf`. Use the `contrib/redlib.conf` as a
template. You can also add the `REDLIB_DEFAULT__{X}` settings explained
above.

When "Proxying using NGINX" where the proxy is on the same machine, you should
guarantee nginx waits for this service to start. Edit
`/etc/systemd/system/redlib.service.d/reverse-proxy.conf`:

```conf
[Unit]
Before=nginx.service
```

## launchd

If you are on macOS, you can use the launchd service available in `contrib/redlib.plist`.

Install it with `cp contrib/redlib.plist ~/Library/LaunchAgents/`.

Load and start it with `launchctl load ~/Library/LaunchAgents/redlib.plist`.

## Building

```
git clone https://github.com/redlib-org/redlib
cd redlib
cargo run
```
