---
title: "Apigee5 : 개발자 포털2"
date: 2022-03-29T13:44:59+09:00
draft: false
weight: 45
---

## 개발자 포털

- [Open-API-Specification](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.0.md)  

### 1. API Document 추가
- API catalog 선택
{{< figure src="/apigee/apigee-tutorial3_1.jpg" >}}

### 2. Portals -> Pages 이동
- API 선택(okd-api-sample)
{{< figure src="/apigee/apigee-tutorial3_2.jpg" >}}

### 3. 우측의 연필 모양 클릭해 편집모드로 변경
{{< figure src="/apigee/apigee-tutorial3_3.jpg" >}}

### 4. API Documentation
- Source API sepc 리스트박스 선택(Select OpenAPI Spec)
{{< figure src="/apigee/apigee-tutorial3_4.jpg" >}}

- JSON 파일 업로드
{{< figure src="/apigee/apigee-tutorial3_5.jpg" >}}
{{< figure src="/apigee/apigee-tutorial3_6.jpg" >}}

- json sample
``` json
{
  "openapi": "3.0.1",
  "info": {
    "title": "okd-sample-API Service",
    "version": "v1"  
  },
  "servers": [
    {
      "url": "https://dotnetexample-okd-tutorial.apps.blackwhale.cloud.hancom.com/"
    }
  ],
  "paths": {
    "/Document": {
      "get": {
        "tags": [
          "Document"
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

### 5. SAVE 선택
{{< figure src="/apigee/apigee-tutorial3_7.jpg" >}}
{{< figure src="/apigee/apigee-tutorial3_8.jpg" >}}

### 6. Live Portal로 이동해 적용 확인
{{< figure src="/apigee/apigee-tutorial3_9.jpg" >}}
{{< figure src="/apigee/apigee-tutorial3_10.jpg" >}}
{{< figure src="/apigee/apigee-tutorial3_11.jpg" >}}
