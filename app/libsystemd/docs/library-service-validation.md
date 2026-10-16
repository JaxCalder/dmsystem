# Library lifecycle validation — 2026-10-16

- Native libsystemd diagnostic: 62/62, including cold loading a DIF-only
  library, a module already enabled through an API dependency, two unit
  instances sharing one module, failed starts, status, removal/re-add and
  refreshed %v paths. Plain library lifecycle tests remain passing.
- Native systemd and service command diagnostics: 1/1 each.
- Full Cortex-M7 build passed, including both lifecycle helper modules.
- STM32F746G-DISCO integration with dmdevfs and dmutc: the RTC event starts
  dmutc@rtc automatically after flash/reset with type=library and pid=0.
  dmutc diagnostic 6/6, RTC 12/12 and RNG 6/6. The UTC test stops/restarts a
  library unit without unloading API consumers and removes/re-adds the RTC
  with both an invalid new path and the actual path.

The cold-load test is separate from the API-imported helper: DIF lookup must
happen after enabling the library. The changed-path test ensures a retained
inactive template instance expands the new event value instead of keeping
an old device path.

Board console evidence is maintained in the dmutc PR alongside its diagnostic.
