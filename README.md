# AI WordPress Server Setup & Optimization

An AI-driven setup guide for turning a **fresh Linux server** into a fast, secure, production-ready WordPress host — and migrating an existing WordPress site onto it.

This project is designed for a server you **already own or rent**, whether it is a VPS, dedicated machine, or a computer running at home. It is **not** a hosting-provider comparison or hardware shopping guide.

Contributions are welcome! If you encounter any issues or find ways to improve the prompt, feel free to submit a pull request to make it even better for everyone.

## What it covers

- **Server discovery:** Inspect the operating system, CPU, RAM, storage, network, and available resources over SSH before choosing settings.
- **Web stack selection:** Explain the trade-offs between LAMP (Apache), LEMP (Nginx), and OpenLiteSpeed, then help the user choose a compatible stack.
- **Database performance:** Configure MariaDB or MySQL with appropriate InnoDB memory allocation, connection limits, slow-query logging, and measured tuning.
- **PHP performance:** Configure PHP-FPM where applicable, OPcache, process limits, and memory settings based on actual server capacity.
- **WordPress migration:** Restore a user-supplied copy of the existing WordPress files and database, safely update URLs when needed, and verify the migrated site.
- **Caching:** Recommend a compatible WordPress caching plugin and provide concrete settings for page caching, Redis object caching, browser caching, and cache invalidation.
- **Cloudflare:** Walk through DNS, SSL/TLS, CDN caching, Cache Rules, WAF, bot protection, and rate limiting, with special handling for logged-in users and WooCommerce.
- **Security:** Harden SSH, firewall rules, file permissions, WordPress access, TLS, and software updates.
- **Operations:** Set up reliable cron jobs, offsite backups, monitoring, logging, and recovery checks.
- **Verification:** Benchmark before and after migration and tuning, check site functionality, and report the measured results.

## Requirements

Before starting, prepare:

1. A **fresh Linux server** with network access and SSH connectivity. Ubuntu is common, but the workflow should adapt to the installed distribution.
2. SSH connection information: hostname/IP, username, port, and an appropriate authentication method. **Never paste private SSH keys or passwords into a chat or repository.**
3. A copy of the existing WordPress **files** (including `wp-content` and any required configuration/custom code).
4. A matching **database export** (`.sql` or a compressed equivalent).
5. The domain name and access to its DNS settings.
6. Cloudflare account access, if Cloudflare will be used.
7. A list of **all existing WordPress plugins**, active and inactive, including versions where possible.

Provide backups through a secure upload or transfer method. Do not commit database dumps, `.env` files, `wp-config.php` containing secrets, SSH keys, or other credentials to Git.

## Recommended AI workflow

### 1. Ask only the essential questions

Confirm SSH access, domain, the availability of WordPress files and a database export, Cloudflare use, and the plugin inventory. Explain LAMP, LEMP, and OpenLiteSpeed briefly and let the user choose or request a recommendation.

Do not ask the user to guess hardware specifications or installed software: inspect the server directly after access is established.

### 2. Audit the clean server

Identify the Linux distribution, CPU architecture, CPU cores, RAM, swap, disks, free space, network interfaces, firewall state, and any preinstalled services. Verify that the server is truly fresh before changing it.

### 3. Propose a configuration

Choose compatible, supported software versions and memory allocations for the actual hardware. Show the proposed web stack, database, caching layers, security measures, backup strategy, and any migration risks. Get approval before making destructive or hard-to-reverse changes.

### 4. Configure and secure the server

Install the selected web stack, PHP extensions, database, Redis if appropriate, TLS, firewall, SSH hardening, and monitoring. Keep SSH access working throughout; test new access before disabling existing methods.

### 5. Restore WordPress

Transfer the files and database securely, create least-privilege database credentials, configure WordPress, repair file permissions, and update site URLs with serialization-safe tools when required. Verify that media, permalinks, plugins, themes, admin access, and scheduled tasks work.

### 6. Configure caching and Cloudflare

Use **one coherent page-caching strategy**, not overlapping plugins and server caches. Choose a cache plugin that actually supports the selected stack: for example, LiteSpeed Cache's server-level page cache requires LiteSpeed-compatible server support. Redis object caching is separate from full-page caching.

Configure Cloudflare DNS, Full (strict) TLS where possible, asset caching, targeted HTML caching if suitable, WAF rules, bot protection, and login rate limiting. Never cache personalized pages, authenticated sessions, checkout, cart, account pages, or other sensitive dynamic responses. Confirm the origin is not unintentionally exposed if origin-lockdown controls are deployed.

### 7. Test and document

Test anonymous and logged-in browsing, admin functionality, forms, media, redirects, scheduled jobs, and WooCommerce flows if installed. Measure response time and load behavior with repeatable tests. Record actual settings, benchmark results, backup/restore procedures, and outstanding issues.

## Important principles

- **Performance must be measured.** Avoid claiming a setting is faster without benchmarking it.
- **Compatibility comes first.** Use supported PHP, database, and web-server versions compatible with the site's plugins and themes.
- **Do not blindly copy tuning values.** Database buffers and PHP worker counts must fit within the server's real memory budget.
- **Do not sacrifice security for speed.** No exposed database ports, weak SSH settings, or public secrets.
- **Avoid outdated advice.** Recheck old tutorials, deprecated directives, and version-specific recommendations against current official documentation.
- **Preserve the existing site.** Take and verify backups before migration, keep a rollback plan, and avoid changing production DNS until the replacement site is tested.
- **Cloudflare features vary by plan.** Check feature availability and current rule syntax rather than assuming every option is free.
- **Be careful with caches.** Use explicit bypass rules and reliable invalidation when content changes.

## Who this is for

Developers, freelancers, agencies, and site owners who want an AI assistant to guide or execute a complete WordPress server setup and migration on their own Linux infrastructure.

## Disclaimer

Server changes can cause downtime or data loss. Review commands before execution, use least-privilege access, maintain independent backups, and confirm the site works before switching DNS or decommissioning the old host. An AI assistant can guide this process, but it cannot guarantee the fastest possible configuration or a secure deployment without testing.

## License

Add a `LICENSE` file with the terms you want before publishing or inviting reuse.
