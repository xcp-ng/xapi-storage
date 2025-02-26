---
title: plugin

language_tabs:
 - json
 - ocaml
 - python

search: true
---
# plugin
The xapi toolstack expects all plugins to support a basic query interface. This means that if you plan to implement both, a volume and a datapath plugin, make sure that both implement the query interface.
## Type definitions
### query_result
```json
{
  "required_cluster_stack": [ "required_cluster_stack" ],
  "configuration": { "configuration": "configuration" },
  "features": [ "features" ],
  "required_api_version": "required_api_version",
  "version": "version",
  "copyright": "copyright",
  "vendor": "vendor",
  "description": "description",
  "name": "name",
  "plugin": "plugin"
}
```
type `query_result` = `struct { ... }`
Properties of this implementation.
#### Members
 Name                   | Type                   | Description                                                                 
------------------------|------------------------|-----------------------------------------------------------------------------
 plugin                 | string                 | Plugin name, used in the XenAPI as SR.type.                                 
 name                   | string                 | Short name.                                                                 
 description            | string                 | Description.                                                                
 vendor                 | string                 | Entity \(e.g. company, project, group\) which produced this implementation. 
 copyright              | string                 | Copyright.                                                                  
 version                | string                 | Version.                                                                    
 required_api_version   | string                 | Minimum required API version.                                               
 features               | string list            | Features supported by this plugin.                                          
 configuration          | (string * string) list | Key/description pairs describing required device\_config parameters.        
 required_cluster_stack | string list            | The plugin requires one of these cluster stacks to be active.               
### srs
```json
[ "srs" ]
[]
```
type `srs` = `string list`

## Interface: `Plugin`
Discover properties of this implementation. Every implementation must support the query interface or it will not be recognised as a storage plugin by xapi.
## Method: `query`
Query this implementation and return its properties. This is  called by xapi to determine whether it is compatible with xapi  and to discover the supported features.

> Client

```json
{ "method": "Plugin.query", "params": [ { "dbg": "dbg" } ], "id": 1 }
```

```ocaml
try
    let query_result = Client.query dbg in
    ...
with Exn (Unimplemented str) -> ...

```

```python

# import necessary libraries if needed
# we assume that your library providing the client is called myclient and it provides a connect method
import myclient

if __name__ == "__main__":
    c = myclient.connect()
    results = c.Plugin.query({ dbg: "string" })
    print(repr(results))
```

> Server

```json
{
  "required_cluster_stack": [
    "required_cluster_stack_1", "required_cluster_stack_2"
  ],
  "configuration": { "field_1": "value_1", "field_2": "value_2" },
  "features": [ "features_1", "features_2" ],
  "required_api_version": "required_api_version",
  "version": "version",
  "copyright": "copyright",
  "vendor": "vendor",
  "description": "description",
  "name": "name",
  "plugin": "plugin"
}
```

```ocaml
try
    let query_result = Client.query dbg in
    ...
with Exn (Unimplemented str) -> ...

```

```python

# import additional libraries if needed

class Plugin_myimplementation(Plugin_skeleton):
    # by default each method will return a Not_implemented error
    # ...

    def query(self, dbg):
        """
        Query this implementation and return its properties. This is
        called by xapi to determine whether it is compatible with xapi
        and to discover the supported features.
        """
        return {"plugin": "string", "name": "string", "description": "string", "vendor": "string", "copyright": "string", "version": "string", "required_api_version": "string", "features": ["string"], "configuration": {"string": "string"}, "required_cluster_stack": ["string"]}
    # ...
```


 Name    | Direction | Type         | Description                        
---------|-----------|--------------|------------------------------------
 dbg     | in        | string       | Debug context from the caller      
 unnamed | out       | query_result | Properties of this implementation. 
## Method: `ls`
\[ls dbg\]: returns a list of attached SRs

> Client

```json
{ "method": "Plugin.ls", "params": [ { "dbg": "dbg" } ], "id": 2 }
```

```ocaml
try
    let srs = Client.ls dbg in
    ...
with Exn (Unimplemented str) -> ...

```

```python

# import necessary libraries if needed
# we assume that your library providing the client is called myclient and it provides a connect method
import myclient

if __name__ == "__main__":
    c = myclient.connect()
    results = c.Plugin.ls({ dbg: "string" })
    print(repr(results))
```

> Server

```json
[ "srs_1", "srs_2" ]
```

```ocaml
try
    let srs = Client.ls dbg in
    ...
with Exn (Unimplemented str) -> ...

```

```python

# import additional libraries if needed

class Plugin_myimplementation(Plugin_skeleton):
    # by default each method will return a Not_implemented error
    # ...

    def ls(self, dbg):
        """
        [ls dbg]: returns a list of attached SRs
        """
        return ["string"]
    # ...
```


 Name | Direction | Type   | Description                   
------|-----------|--------|-------------------------------
 dbg  | in        | string | Debug context from the caller 
 srs  | out       | srs    | The attached SRs              
## Method: `diagnostics`
Returns a printable set of backend diagnostic information.  Implementations are encouraged to include any data which will  be useful to diagnose problems. Note this data should not  include personally-identifiable data as it is intended to be   automatically included in bug reports.

> Client

```json
{ "method": "Plugin.diagnostics", "params": [ { "dbg": "dbg" } ], "id": 3 }
```

```ocaml
try
    let diagnostics = Client.diagnostics dbg in
    ...
with Exn (Unimplemented str) -> ...

```

```python

# import necessary libraries if needed
# we assume that your library providing the client is called myclient and it provides a connect method
import myclient

if __name__ == "__main__":
    c = myclient.connect()
    results = c.Plugin.diagnostics({ dbg: "string" })
    print(repr(results))
```

> Server

```json
"diagnostics"
```

```ocaml
try
    let diagnostics = Client.diagnostics dbg in
    ...
with Exn (Unimplemented str) -> ...

```

```python

# import additional libraries if needed

class Plugin_myimplementation(Plugin_skeleton):
    # by default each method will return a Not_implemented error
    # ...

    def diagnostics(self, dbg):
        """
        Returns a printable set of backend diagnostic information.
        Implementations are encouraged to include any data which will
        be useful to diagnose problems. Note this data should not
        include personally-identifiable data as it is intended to be
        automatically included in bug reports.
        """
        return "string"
    # ...
```


 Name        | Direction | Type   | Description                                                         
-------------|-----------|--------|---------------------------------------------------------------------
 dbg         | in        | string | Debug context from the caller                                       
 diagnostics | out       | string | A string containing loggable human-readable diagnostics information 
## Errors
### exnt
```json
[ "Unimplemented", "exnt" ]
```
type `exnt` = `variant { ... }`

#### Constructors
 Name          | Type   | Description 
---------------|--------|-------------
 Unimplemented | string |             