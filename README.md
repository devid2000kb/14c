# Redmi 14C (lake) modules

Magisk modules for the Redmi 14C 4G / POCO C75 / Redmi A3 Pro (lake, MT6768,
Android 14) used for root hiding, Play Integrity and keybox attestation.

These are the same module sources as the 15C project, rebuilt for the 14C
repository.

## Modules

| id | name | version | purpose |
| --- | --- | --- | --- |
| adminupdate | AdminUpdate | v6.7 (540) | bank/root hiding, TrickyStore target sync, auto PIF rotation, silent keybox updates, OTA module updates |
| tricky_store | TEESimulator-RS | v6.0.1-282 (284) | software simulation of hardware-backed key pairs and attestation |
| playintegrityfix | Play Integrity Fork | v19 (190003) | fixes Play Integrity verdicts on Android 7+ |
| zygisksu | NeoZygisk | v2.4 (303) | Zygote injection with ptrace |
| zygisk_nohello | Nohello | v0.0.7 (53) | Zygisk module to hide root |

## Requirements

- Unlocked bootloader on the 14C (see the unlock kit in the 14C workspace).
- Magisk Alpha 31100 or newer, root working.
- Zygisk enabled in Magisk.

## Install order

1. adminupdate
2. tricky_store
3. playintegrityfix
4. zygisksu
5. zygisk_nohello

Install all five, then reboot once. Magisk: Modules, Install from storage. Or
with root: `magisk --install-module <zip>`.

## Keybox

AdminUpdate fetches the keybox from this repository on boot. The active keybox
is the verified shared one, state 1794414030, SHA-256:

    c51e3b0300cbd1747727a45cde53100aa428007109112502fc6b96b1dae20324

It is the same keybox used by the 15C project. The assets are `assets/state.txt`
and the encoded `assets/sys.dat`.

Manual path if needed: copy `keybox.xml` to `/data/adb/tricky_store/keybox.xml`
with root and reboot.

## Updates

The manifest and module zips in this repository are the update source for
AdminUpdate on 14C phones. The publisher rebuilds them from the WORK folder and
bumps versions when the sources change.

## Credits

- Magisk and Magisk Alpha
- AdminUpdate
- TEESimulator-RS by JingMatrix and Enginex0
- Play Integrity Fork by osm0sis and chiteroman
- NeoZygisk by JingMatrix
- Nohello by mhmrdd

## Warning

An unlocked bootloader and a keybox can be detected. Bank and DRM apps may still
refuse to run. Test on your own device first. Do not flash efuse.img and do not
run official ROM scripts on an unlocked 14C; see the warning file in the 14C
workspace.
