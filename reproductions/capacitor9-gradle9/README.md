# Reproduce Android Gradle warnings with Capacitor 9

Use Node 24, JDK 21, Gradle 9.8.2 and Android SDK 37. Set `JAVA_HOME` and
`ANDROID_HOME` for those installations. Run these commands from this directory.

```sh
npm install --legacy-peer-deps --ignore-scripts --no-audit --no-fund
gradle help --warning-mode all
gradle :crashlytics:compileDebugJavaWithJavac --warning-mode all
```

Use the legacy peer resolver for this reproduction because npm excludes prereleases
from ordinary stable peer ranges.

The first Gradle command reports implicit parent project property lookups from
the Crashlytics and Barcode Scanning modules. The second also compiles
Crashlytics and fails at `PluginCall.hasOption("value")`, a method removed
in Capacitor 9.
