==================================================
 Hookflash AWIN Last Click Identifier (README)
==================================================

1. OVERVIEW
-----------
The Hookflash AWIN Last Click Identifier is a custom Google Tag Manager template
that sets a cookie attributing a visitor’s last-click source to AWIN (“aw”),
organic, or other paid channels. It addresses the following points:

• Stops checking other source values after encountering a valid match 
  (so the correct channel is retained).
• Matches AWIN source using exact or partial checks (depending on your 
  configuration) to avoid confusion with parameters like 'gclid' that might 
  contain the substring "aw".

2. HOW IT WORKS
---------------
1) Referrer Check:
   - If the visitor is already coming from the same domain, the tag does 
     nothing and completes. (We only want to attribute new arrivals, not 
     internal navigation.)

2) URL Parameters Check:
   - Looks for a “awaid” parameter. If found, sets the cookie to "aw" and stops.
   - Otherwise, searches for “paid channel” parameters (e.g., utm_source) 
     specified in the template settings.

3) AWIN vs. OTHER Source:
   - If any parameter value matches the “awinSource” list (e.g., “aw”, “awin”, 
     “aff”), sets cookie to "aw".
   - Otherwise, sets cookie to “other” if a paid channel parameter was found.

4) Organic Filter:
   - If "organicFilter" is enabled, checks the referrer for known search 
     engines (Google, Bing, Yahoo, Yandex, DuckDuckGo).
   - If a match is found, sets cookie to “organic”.

5) Direct:
   - If no parameters are matched and the referrer is not a known search engine, 
     sets the cookie to “direct”.

6) Cookie Lifetime:
   - Determined by the “cookiePeriod” (in days). If set to 0, a session cookie 
     is used (expires when the browser closes).

3. TEMPLATE PARAMETERS
----------------------
• Cookie name (cookieName)
  - Name of the cookie to set.
  - Allowed characters: letters, numbers, underscores, hyphens.

• Cookie length (cookiePeriod)
  - The duration (in days) the cookie is kept. 
  - If set to 0, a session-only cookie is used.

• Used Source Parameters (sourceParameters)
  - A comma-separated list of URL parameter names (e.g., utm_source, 
    utm_medium, gclid) used to detect a “paid channel” click.

• Awin Source Values (awinSource)
  - A comma-separated list of strings that identify AWIN traffic 
    (e.g., “aw”, “awin”, “aff”).

• Organic Filter (organicFilter)
  - If checked, traffic from recognized search engines 
    (e.g., Google, Bing) is labeled “organic.”

• Overwrite Cookie Domain (overwriteCookieDomain)
  - If checked, the domain of the cookie is overwritten with the 
    “AwinChannelCookie Domain” field below.

• AwinChannelCookie Domain (awinChannelCookieDomain)
  - If the “Overwrite Cookie Domain” box is checked, provide the domain 
    to use (e.g., .example.com).

4. INSTALLATION & USAGE
-----------------------
1) Import the Template
   - In GTM, go to Templates > New > Import.
   - Copy/paste the template’s code (the SANDBOXED_JS_FOR_WEB_TEMPLATE block 
     and the associated metadata) into the custom template builder.
   - Approve the requested permissions.

2) Configure the Tag
   - Create a new tag: New Tag > Tag Configuration > Hookflash AWIN Last 
     Click Identifier.
   - Fill in or adjust:
       * Cookie name
       * Cookie length
       * Used Source Parameters
       * Awin Source Values
       * Organic Filter (checkbox)
       * Overwrite Cookie Domain (checkbox)
       * AwinChannelCookie Domain

3) Assign a Trigger
   - Typically fired on All Pages or similar triggers, so the template checks 
     new arrivals on each page load.

4) Preview & Publish
   - Test in Preview mode.
   - Check your browser’s Developer Tools -> Application (or Storage) tab 
     to confirm the cookie is being set.
   - Once verified, publish your container.

5. RELEASE NOTES
----------------
• Version 1
  - Initial Release.
  - Resolves overwriting the cookie after a match is found.
  - Switches from broad "contains" checks to more precise AWIN matching 
    for URL parameters.

6. TERMS OF SERVICE
-------------------
By creating or modifying this file you agree to Google Tag Manager’s 
Community Template Gallery Developer Terms of Service, available at:
https://developers.google.com/tag-manager/gallery-tos

7. EXAMPLE CONFIGURATION
------------------------
Example Setup:
• Cookie name: AwinChannelCookie
• Cookie length: 30 (days)
• Used Source Parameters: utm_source,utm_medium,gclid,fbclid,msclkid
• Awin Source Values: aw,awin,aff
• Organic Filter: true (checked)
• Overwrite Cookie Domain: false (unchecked)
• AwinChannelCookie Domain: (leave blank)

In this example, a cookie named “AwinChannelCookie” is set for 30 days whenever 
someone arrives from an external domain. If the URL contains “awaid” or if one 
of the source parameters includes “aw” from your `awinSource` list, it marks 
the visitor as “aw.” If they arrive from a recognized search engine (with 
organicFilter enabled), it marks them “organic.” Otherwise, it sets “other” or 
“direct.”

====================================
END OF README
====================================
