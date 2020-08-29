--- services/APIHausey/incoming_webhooks/ApiHausey/source.js
+++ services/APIHausey/incoming_webhooks/ApiHausey/source.js
@@ -1,32 +1,6 @@
-// This function is the webhook's request handler.
-exports = function(payload, response) {
-    // Data can be extracted from the request as follows:
-
-    // Query params, e.g. '?arg1=hello&arg2=world' => {arg1: "hello", arg2: "world"}
-    const {arg1, arg2} = payload.query;
-
-    // Headers, e.g. {"Content-Type": ["application/json"]}
-    const contentTypes = payload.headers["Content-Type"];
-
-    // Raw request body (if the client sent one).
-    // This is a binary object that can be accessed as a string using .text()
-    const body = payload.body;
-
-    console.log("arg1, arg2: ", arg1, arg2);
-    console.log("Content-Type:", JSON.stringify(contentTypes));
-    console.log("Request body:", body);
-
-    // You can use 'context' to interact with other Realm features.
-    // Accessing a value:
-    // var x = context.values.get("value_name");
-
-    // Querying a mongodb service:
-    // const doc = context.services.get("mongodb-atlas").db("dbname").collection("coll_name").findOne();
-
-    // Calling a function:
-    // const result = context.functions.execute("function_name", arg1, arg2);
-
-    // The return value of the function is sent as the response back to the client
-    // when the "Respond with Result" setting is set.
-    return  "Hello World!";
+  
+exports = function(payload) {
+  const mongodb = context.services.get("mongodb-atlas");
+  const mycollection = mongodb.db("HauseyTaruma").collection("Protocol_Hamilton");
+  return mycollection.find({}).toArray();
 };
_________________________


--- secrets.json
+++ secrets.json
@@ -4,6 +4,7 @@
     },
     "services": {
         "APIHausey": {},
+        "APIHausey_Post": {},
         "mongodb-atlas": {}
     }
 }
--- services/APIHausey_Post/config.json
+++ services/APIHausey_Post/config.json
@@ -1 +1,8 @@
+{
+    "id": "5f4a01d1bfb90ac620863b6b",
+    "name": "APIHausey_Post",
+    "type": "http",
+    "config": {},
+    "version": 1
+}
 
--- services/APIHausey_Post/incoming_webhooks/webhook1/config.json
+++ services/APIHausey_Post/incoming_webhooks/webhook1/config.json
@@ -1 +1,15 @@
+{
+    "id": "5f4a01efe869aaa9be5614e6",
+    "name": "webhook1",
+    "run_as_authed_user": false,
+    "run_as_user_id": "",
+    "run_as_user_id_script_source": "",
+    "options": {
+        "httpMethod": "POST",
+        "validationMethod": "NO_VALIDATION"
+    },
+    "respond_result": true,
+    "fetch_custom_user_data": false,
+    "create_user_on_auth": false
+}
 
--- services/APIHausey_Post/incoming_webhooks/webhook1/source.js
+++ services/APIHausey_Post/incoming_webhooks/webhook1/source.js
@@ -1 +1,19 @@
+exports = async function (payload) {
+  
+  var body = {};
+  var result = {};
+  if (payload.body) {
+    console.log (JSON.stringify(payload.body));
+    body = EJSON.parse (payload.body.text());
+    console.log(JSON.stringify("body.input"));
+    console.log(JSON.stringify(body));
+    
+    var proyects = await context.services.get("mongodb-atlas").db ("HauseyTaruma").collection("Protocol_Hamilton");
+    var doc = await proyects.insertOne(body);
+    console.log (JSON.stringify("return document"));
+    console.log(JSON.stringify(doc));
+  }
+  return doc;
+  }
+;
