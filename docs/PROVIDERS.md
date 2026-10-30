# DrKozol provider integration

Official downloads and feedback: https://github.com/SpecterLogic/Drkozol

## Subscription compatibility

Use an HTTPS subscription returning plain protocol links, Base64-encoded protocol links, or supported Xray JSON configurations. Do not return the panel's HTML account page, Clash YAML or sing-box JSON as an Xray subscription. Protocol and transport support depends on the bundled core.

The default Android User-Agent is `DrKozol/Android`. A user may override it per provider. Recognize the case-insensitive prefix `DrKozol/` when selecting your V2Ray/Xray-compatible output. Do not require the client to impersonate another application's User-Agent.

Supported optional response metadata includes `profile-title` (plain or `base64:` UTF-8), `subscription-userinfo`, `profile-update-interval` in hours, `profile-web-page-url`, and `announce` / `profile-announce`. Explicit user choices for provider naming and update intervals remain authoritative. The optional `routing` header supports the compatible Happ routing profile format; it is not arbitrary code execution.

## Add a subscription button

Generate this link on the provider's own subscription page or bot:

```text
drkozol://install-sub?url=URL_ENCODED_SUBSCRIPTION_URL
```

Percent-encode the complete subscription URL, including its query parameters and fragment, exactly once. Use the generated link for the button and its QR code. Do not place a customer's real subscription in public documentation, GitHub Issues or screenshots.

The Android package is `com.drkozol.client`. Downloads: https://github.com/SpecterLogic/Drkozol/releases/latest

## Panels

| Panel | Integration path | Status |
| --- | --- | --- |
| 3x-ui | Expose its V2Ray/Xray subscription output and add the import button to the user subscription page | Standards-based integration; panel-side listing requires its maintainer or operator |
| Marzban | Use V2Ray links or its explicit V2Ray JSON output; add an import button to the subscription template | The panel's current generic User-Agent fallback returns V2Ray links |
| PasarGuard | Select a V2Ray-compatible format in the application/subscription settings; register the DrKozol import link in the configurable app list | Panel provides configurable application settings and a subscription apps endpoint |
| Hiddify Manager | Use its V2Ray/Xray-compatible subscription, not the sing-box-only output; add the import button to the account page | Standards-based integration; live deployment verification still required |

This describes client interoperability, not official endorsement or an upstream inclusion claim. Test your actual panel version, output format, supported transports, expiry/traffic metadata, refresh behavior and QR import before advertising compatibility.

## Operator checklist

1. Import a fresh test account using the button and QR.
2. Verify provider name, usage, expiry and manual refresh.
3. Connect each protocol and transport you advertise using Real Delay and an actual network request.
4. Change subscription contents and confirm refresh preserves the user's choices.
5. Check expired/disabled accounts and empty subscription responses.

## Upstream references

- [3x-ui](https://github.com/MHSanaei/3x-ui)
- [Marzban subscription negotiation](https://github.com/Gozargah/Marzban/blob/master/app/routers/subscription.py)
- [PasarGuard subscription endpoints](https://github.com/PasarGuard/panel/blob/main/app/routers/subscription.py)
- [PasarGuard application settings](https://github.com/PasarGuard/panel/blob/main/app/models/settings.py)
- [Hiddify Manager](https://github.com/hiddify/Hiddify-Manager)
