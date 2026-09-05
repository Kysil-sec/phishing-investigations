# SIMIT Phishing Investigation

Documenting the analysis of a phishing campaign impersonating Colombia's traffic-fines system.

## Status

Completed investigation.

## Overview

An SMS phishing campaign impersonating SIMIT used a shortened URL to direct victims to a fake traffic-fine payment website.

The site used a fabricated fine, an urgent payment deadline, and a supposed 50% discount to encourage victims to submit personal and payment information.

I analyzed the site using browser developer tools, investigated its infrastructure, and reported the phishing operation to Cloudflare.

## Initial Discovery

The phishing SMS was received by a family member.

The message claimed that the recipient was in a legal collection process and at risk of having their assets seized.

It included a shortened URL:

`dcto-vial[.]co/2O26-`

The URL redirected to a site impersonating SIMIT:

`simit-multas[.]col-online-pagos[.]cc`

An important initial indicator was that the recipient did not own a vehicle and had no obvious reason to receive a traffic-fine payment notice.

## Technical Analysis

I used browser developer tools to inspect the phishing page and its network activity.

The site loaded a JavaScript file:

`script.js?v=17`

The script contained references to backend endpoints including:

`api.php`

`pse.php`

The phishing workflow requested:

* Identification information
* Address information
* Payment information

The site also exhibited conditional redirect behavior.

When accessed with a non-mobile User-Agent, it redirected to Google. Changing the User-Agent to an iPhone allowed the phishing workflow to load.

This behavior was consistent with cloaking intended to make automated analysis more difficult.

## Reporting

I reported the phishing domain to Cloudflare.

The report included:

* The phishing domain
* The shortened URL
* The impersonation of SIMIT
* The observed JavaScript behavior
* The backend endpoints
* The conditional redirect behavior

Cloudflare confirmed that the report had been forwarded to the website owner and the relevant hosting provider.

Cloudflare also stated that access to the reported URLs had been restricted.

## Result

The reported phishing site is no longer accessible.

## Lessons Learned

* Social-engineering indicators can help identify phishing before technical analysis.
* Browser developer tools are useful for understanding phishing workflows.
* User-Agent-based cloaking can affect what a researcher sees.
* CDN/proxy providers and hosting providers may be separate entities.
* Abuse reporting can lead to infrastructure being restricted.

## Safety Notes

No real payment information or credentials were submitted during the investigation.

Sensitive information belonging to third parties has been omitted.
