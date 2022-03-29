---
title: "Apigee7 : API Proxies Demo"
date: 2022-03-29T13:45:03+09:00
draft: false
weight: 47
---

### Create New
{{< figure src="/apigee/apigee-tutorial5_1.jpg" >}}

### Reverse Proxy 선택
{{< figure src="/apigee/apigee-tutorial5_2.jpg" >}}

### Proxy details
{{< figure src="/apigee/apigee-tutorial5_3.jpg" >}}

```
Name: okd-api
Base path: okd-api
Target: https://dotnetexample-okd-tutorial.apps.blackwhale.cloud.hancom.com/Document
```

{{< figure src="/apigee/apigee-tutorial5_4.jpg" >}}

```
Security(Authorization) : API Key
Quota: Impose quotas per App
Security(Browser) : Add CORS headers
```
#### Summary
{{< figure src="/apigee/apigee-tutorial5_5.jpg" >}}

#### Edit Proxy
{{< figure src="/apigee/apigee-tutorial5_6.jpg" >}}

#### Overview
{{< figure src="/apigee/apigee-tutorial5_7.jpg" >}}

#### eval(개발환경) deploy
{{< figure src="/apigee/apigee-tutorial5_8.jpg" >}}

- Deploy 선택
{{< figure src="/apigee/apigee-tutorial5_9.jpg" >}}

#### DEVELOP 탭 확인
{{< figure src="/apigee/apigee-tutorial5_10.jpg" >}}

### PreFlow
```
[Policies]
- Add CORS
- Impose Quota
- Remove Query Param apikey
- Verify API Key
```

---
### API Products 추가(Create New 선택)
{{< figure src="/apigee/apigee-tutorial5_11.jpg" >}}

### Product details 입력
{{< figure src="/apigee/apigee-tutorial5_12.jpg" >}}

```
Name: okd-api-product
Display Name: Demo API
Environment: eval
Access: Public
```

#### Oprations 추가(ADD AN OPERATION)
{{< figure src="/apigee/apigee-tutorial5_13.jpg" >}}

```
API Proxy : okd-api
Operation: /okd-api
Methods: 모두 선택
```

#### Save를 눌러 저장한다. 
{{< figure src="/apigee/apigee-tutorial5_14.jpg" >}}

#### Potal로 이동(API catalog 선택)
{{< figure src="/apigee/apigee-tutorial5_15.jpg" >}}

#### API Documenttation 추가
[API URL](https://spsenti2023.duckdns.org/okd-api)
[sample json]
``` json
{
  "openapi": "3.0.1",
  "info": {
    "title": "okd-sample-API Service",
    "version": "v1"  
  },
  "servers": [
    {
      "url": "https://spsenti2023.duckdns.org/"
    }
  ],
  "paths": {
    "/Document": {
      "get": {
        "tags": [
          "okd-api"
        ],
        "operationId": "GetDocument",
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "text/plain": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/DocumentModel"
                  }
                }
              },
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/DocumentModel"
                  }
                }
              },
              "text/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/DocumentModel"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/WeatherForecast": {
      "get": {
        "tags": [
          "WeatherForecast"
        ],
        "operationId": "GetWeatherForecast",
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "text/plain": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WeatherForecast"
                  }
                }
              },
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WeatherForecast"
                  }
                }
              },
              "text/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WeatherForecast"
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "DocumentModel": {
        "type": "object",
        "properties": {
          "date": {
            "type": "string",
            "format": "date-time"
          },
          "name": {
            "type": "string",
            "nullable": true
          },
          "summary": {
            "type": "string",
            "nullable": true
          }
        },
        "additionalProperties": false
      },
      "WeatherForecast": {
        "type": "object",
        "properties": {
          "date": {
            "type": "string",
            "format": "date-time"
          },
          "temperatureC": {
            "type": "integer",
            "format": "int32"
          },
          "temperatureF": {
            "type": "integer",
            "format": "int32",
            "readOnly": true
          },
          "summary": {
            "type": "string",
            "nullable": true
          }
        },
        "additionalProperties": false
      }
    }
  }
}
```
