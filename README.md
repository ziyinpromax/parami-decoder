# Parami Decoder

Standalone Android app (package `com.parami.decoder`, version 1.0) that
decodes NetMod locked links (`nm-<proto>://...`) into standard link/config
text for copying.

**Decode-only, fully offline.** The app has no connect/VPN function, no
network use, and requests no permissions at all (not even INTERNET).
Paste a link, tap Decode, copy the result.

Supported schemes (13): nm-ssh, nm-vless, nm-vmess, nm-ss, nm-trojan,
nm-trojan-go, nm-ssr, nm-socks, nm-dns, nm-http, nm-hysteria2,
nm-wireguard, nm-xray-json.

Presentation: nm-vmess shows the decrypted JSON as-is; nm-vless shows
`vless://` + body; nm-socks shows `socks://` + body; every other scheme
shows the decrypted text as-is.

Errors are shown as plain Burmese lines, never a crash: non-nm- input,
bad base64, and all-keys-fail each have their own message.

## Build

```sh
./build.sh
```

Pure Java, zero dependencies. The script runs the desktop round-trip
self-test first (synthesized vectors only, no real sample), then builds,
zipaligns, signs, and verifies `ParamiDecoder.apk`. The signing keystore
is generated once and kept in this directory for future updates.

## Keys

The decode keys are embedded in the app only in their obfuscated form
and de-obfuscated at runtime. No key material is printed in this README,
in code comments, or in build output.
