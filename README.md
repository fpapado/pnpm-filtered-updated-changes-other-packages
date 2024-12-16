# Instructions

Ensure that the specified node and pnpm are used (tested with pnpm@9.15.0):

1. `nvm use`
2. `corepack enable`
3. `pnpm install`

Update react to latest only for pakage `a` (such that react@19.0.0 is resolved):

```shell
pnpm --filter a update --latest react
```

Observe that the lockfile has changed for package `b` as well:

```diff
diff --git a/packages/a/package.json b/packages/a/package.json
index 64bd07f..1dfb9e1 100644
--- a/packages/a/package.json
+++ b/packages/a/package.json
@@ -10,6 +10,6 @@
   "author": "",
   "license": "ISC",
   "dependencies": {
-    "react": "18.3.0"
+    "react": "19.0.0"
   }
 }
diff --git a/pnpm-lock.yaml b/pnpm-lock.yaml
index b3fe1d8..0cbf890 100644
--- a/pnpm-lock.yaml
+++ b/pnpm-lock.yaml
@@ -11,36 +11,21 @@ importers:
   packages/a:
     dependencies:
       react:
-        specifier: 18.3.0
-        version: 18.3.0
+        specifier: 19.0.0
+        version: 19.0.0

   packages/b:
     dependencies:
       react:
         specifier: 18.3.0
-        version: 18.3.0
+        version: 19.0.0

 packages:

-  js-tokens@4.0.0:
-    resolution: {integrity: sha512-RdJUflcE3cUzKiMqQgsCu06FPu9UdIJO0beYbPhHN4k6apgJtifcoCtT9bcxOpYBtpD2kCM6Sbzg4CausW/PKQ==}
-
-  loose-envify@1.4.0:
-    resolution: {integrity: sha512-lyuxPGr/Wfhrlem2CL/UcnUc1zcqKAImBDzukY7Y5F/yQiNdko6+fRLevlw1HgMySw7f611UIY408EtxRSoK3Q==}
-    hasBin: true
-
-  react@18.3.0:
-    resolution: {integrity: sha512-RPutkJftSAldDibyrjuku7q11d3oy6wKOyPe5K1HA/HwwrXcEqBdHsLypkC2FFYjP7bPUa6gbzSBhw4sY2JcDg==}
+  react@19.0.0:
+    resolution: {integrity: sha512-V8AVnmPIICiWpGfm6GLzCR/W5FXLchHop40W4nXBmdlEceh16rCN8O8LNWm5bh5XUX91fh7KpA+W0TgMKmgTpQ==}
     engines: {node: '>=0.10.0'}

 snapshots:

-  js-tokens@4.0.0: {}
-
-  loose-envify@1.4.0:
-    dependencies:
-      js-tokens: 4.0.0
-
-  react@18.3.0:
-    dependencies:
-      loose-envify: 1.4.0
+  react@19.0.0: {}
```

`pnpm ls` shows similar output

```shell
pnpm ls -r react
Legend: production dependency, optional only, dev only

a@1.0.0 /Users/fotis/pnpm-filtered-updated-changes-other-packages/packages/a

dependencies:
react 19.0.0

b@1.0.0 /Users/fotis/pnpm-filtered-updated-changes-other-packages/packages/b

dependencies:
react 19.0.0
```
