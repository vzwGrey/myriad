# Myriad

Arbitrary code execution server using Docker.  

## Install

- Install [Stack 2+](https://docs.haskellstack.org/en/stable/README/)
- Run `stack install`, a `myriad` executable will be installed

## Running

- Make sure the configuration is filled out, see `config.dhall` for an example
- Run `myriad --config path/to/config.dhall`

## Endpoints

### **GET** `/languages`
List of enabled languages.  
Example response:  

```json
["haskell", "javascript"]
```

### **POST** `/eval`
Evaluate code.  
JSON payload with `language` and `code` keys.  
The `language` is as in the name of a subfolder in the `languages` directory.  
Example payload:  

```json
{ "language": "haskell", "code": "main = print (1 + 1)" }
```

Example response:  

```json
{ "result": "2\n" }
```

Errors with 404 if `language` is not found, `504` if evaluation timed out, or `500` if evaluation failed for other reasons.  
