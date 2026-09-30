# Plugin Solar Compare

Consumer solar comparisons for the United Kingdom, provided by Opus Leads Ltd.
This Cursor-format plugin connects to the existing public Plugin Solar Compare
MCP service. No login or API key is required for the comparison service.

## Capabilities

The single read-only `compare_solar` tool compares plug-in solar kits, DIY
options and professionally installed solar using the website's matching rules.
It asks for missing household details and returns up to five organic matches,
with recorded prices where available, caveats, supplier links and a link to the
full website comparison. Results retain the website's ordering.

This is a consumer connector. It cannot buy products, send enquiries, manage
business listings or subscriptions, or access private business accounts.

## Configuration

`mcp.json` points to `https://pluginsolarcompare.co.uk/mcp`, a server-side
Streamable HTTP endpoint. The package contains no credentials, local commands,
scripts, hooks or installation dependencies.

## Example Requests

- Help me compare plug-in solar kits for my garden in the UK.
- My postcode is BS1 1AD and I own a house. What else do you need?
- Compare professionally installed solar and explain which prices need a quote.

## Handling Results

- Send only answers the user has provided. Ask the questions returned by the
  tool rather than guessing their postcode, property or preferences.
- Calls are stateless: include all previously supplied answers in later calls.
- Use the allowed values from the tool schema and returned questions. Do not
  send names, email addresses, credentials or payment information.
- Preserve result order, eligibility labels, observation dates and uncertainty.
  Recorded prices are not guaranteed live offers, stock or final delivered costs.
- Quote-required prices and zero matches are valid results. Ask before changing
  the user's preferences; never invent matches, prices or completed actions.
- Comparison results are not electrical approval or guaranteed suitability.
  Keep the supplier's conditions and the service's caveats visible.
- Provide the returned full comparison link so users can continue on the site.

## Service Limits

Requests are limited to 8 KB, 30 requests/minute/IP per Cloudflare location and
a 15-second server timeout. Clients sharing a proxy IP share that allowance.
Respect HTTP 429 and its Retry-After header; do not retry in a tight loop.
The endpoint supports POST; GET 405 is expected. Server-side clients work
without an Origin header. Cross-origin browser calls are intentionally rejected.

## Links

- [Website](https://pluginsolarcompare.co.uk/)
- [AI access documentation](https://pluginsolarcompare.co.uk/ai-access)
- [Support](https://pluginsolarcompare.co.uk/contact)
- [Privacy](https://pluginsolarcompare.co.uk/privacy)
- [Terms](https://pluginsolarcompare.co.uk/terms)

## Release Status

Source availability does not imply marketplace approval or listing. The remote
service has passed separate MCP protocol tests; actual Grok Bot integration
testing is still required. This package does not claim platform certification.

## Licence

The configuration files and this README are MIT-licensed; see [LICENSE](LICENSE).
The logo in `assets/icon.svg` is excluded from that licence. Logo and brand
rights are reserved by Opus Leads Ltd. No trademark rights are granted by the
MIT licence. The hosted service, website source and supplier dataset are not
part of this repository or its open-source licence.
