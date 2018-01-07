## Permission Settings for Result Exporting


Administrator for KAP server can control the permissions of exporting query results by setting the config items of `kap.web.export.allow.admin` and `kap.web.export.allow.other` in `conf/kylin.properties`, both for ADMIN and non-ADMIN users of KAP.

1. After setting `kap.web.export.allow.admin` to `false`, the button for exporting query results will not be shown on the insight page for ADMIN users. ADMIN users will also not be allowed to call the restful api for exporting query result;
2. After setting `kap.web.export.allow.other` to `false`, the button for exporting query results will not be shown on the insight page for non-ADMIN users. Non-ADMIN users will also not be allowed to call the restful api for exporting query result.
