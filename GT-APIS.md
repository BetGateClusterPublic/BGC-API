# GT APIs definition

- [Translation APIs](#translation-apis)

## Translation API
Body of request: Array of selection keys in format "Sport_OutcomeSelectionKey" - for example:
- ["Football_[14,[3],[0],66,11,[]]"]
- ["Football_[14,[3],[0],66,11,[]]", "F_[2,[],[0],1,3,[]]"]

<details>
  <summary>Request JSON schema:</summary>

```json
{
  "openapi":"3.0.1",
  "info":{
    "title":"GT Translations",
    "version":"v1"
  },
  "servers":[
    {
      "url":"https://public-api-stage-hz.betgate.dev"
    }
  ],
  "paths":{
    "/api/gt/translate/selections/{language}":{
      "post":{
        "tags":[
          "Translation"
        ],
        "summary":"Translate selections on all languages.",
        "parameters":[
          {
            "name":"language",
            "in":"path",
            "description":"Language of translation",
            "required":true,
            "schema":{
              "type":"string"
            }
          }
        ],
        "requestBody":{
          "description":"Array of selection keys in format \"F_[14,[3],[0],66,11,[]]\"",
          "content":{
            "application/json-patch+json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            },
            "application/json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            },
            "text/json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            },
            "application/*+json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            }
          }
        },
        "responses":{
          "200":{
            "description":"Success"
          },
          "400":{
            "description":"Bad Request",
            "content":{
              "text/plain":{
                "schema":{
                  "$ref":"#/components/schemas/ProblemDetails"
                }
              },
              "application/json":{
                "schema":{
                  "$ref":"#/components/schemas/ProblemDetails"
                }
              },
              "text/json":{
                "schema":{
                  "$ref":"#/components/schemas/ProblemDetails"
                }
              }
            }
          },
          "500":{
            "description":"Server Error"
          }
        }
      }
    },
    
    "/api/gt/translate/selections":{
      "post":{
        "tags":[
          "Translation"
        ],
        "summary":"Translate selections on all languages.",
        "requestBody":{
          "description":"Array of selection keys in format \"F_[14,[3],[0],66,11,[]]\"",
          "content":{
            "application/json-patch+json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            },
            "application/json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            },
            "text/json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            },
            "application/*+json":{
              "schema":{
                "type":"array",
                "items":{
                  "type":"string"
                }
              }
            }
          }
        },
        "responses":{
          "200":{
            "description":"Success"
          },
          "400":{
            "description":"Bad Request",
            "content":{
              "text/plain":{
                "schema":{
                  "$ref":"#/components/schemas/ProblemDetails"
                }
              },
              "application/json":{
                "schema":{
                  "$ref":"#/components/schemas/ProblemDetails"
                }
              },
              "text/json":{
                "schema":{
                  "$ref":"#/components/schemas/ProblemDetails"
                }
              }
            }
          },
          "500":{
            "description":"Server Error"
          }
        }
      }
    }
  },
  "components":{
    "schemas":{
      "ProblemDetails":{
        "type":"object",
        "properties":{
          "type":{
            "type":"string",
            "nullable":true
          },
          "title":{
            "type":"string",
            "nullable":true
          },
          "status":{
            "type":"integer",
            "format":"int32",
            "nullable":true
          },
          "detail":{
            "type":"string",
            "nullable":true
          },
          "instance":{
            "type":"string",
            "nullable":true
          }
        },
        "additionalProperties":{

        }
      }
    }
  }
}
```
</details>

### POST /api/translate/selections/{language}
Retrieve translation for requested language.

```
curl -X POST https://public-api-stage-hz.betgate.dev/apt/gt/translate/selections/en -H "Content-Type: application/json" -H "X-Api-Key: 6b4314aa-638b-4f8b-a0eb-d17f830fc32a" "[\"Football_[14,[3],[0],66,11,[]]\",\"Basketball_[145,[],[0],1,3,[]]\"]"
```
```json
[
  {
    "key": "Football_[14,[3],[0],66,11,[]]",
    "item": {
      "market": [
        "Shots on target. Race to N",
        ""
      ],
      "text": "3: {Team1}",
      "competitor": [],
      "textShort": "3: 1"
    },
    "isTranslated": false
  },
  {
    "key": "Basketball_[145,[],[0],1,3,[]]",
    "item": {
      "market": [
        "To win including overtime",
        ""
      ],
      "text": "{Team2}",
      "competitor": [],
      "textShort": "2"
    },
    "isTranslated": false
  }
]
```

### POST /api/translate/selections
Retrieve translations for all languages.

```
curl -X POST https://public-api-stage-hz.betgate.dev/apt/gt/translate/selections -H "Content-Type: application/json" -H "X-Api-Key: 6b4314aa-638b-4f8b-a0eb-d17f830fc32a" "[\"Football_[14,[3],[0],66,11,[]]\",\"Basketball_[145,[],[0],1,3,[]]\"]"
```
```json
[
  {
    "key": "Football_[14,[3],[0],66,11,[]]",
    "item": {
      "key": null,
      "market": {
        "ru": [
          "Удары в створ. Первый до N",
          ""
        ],
        "en": [
          "Shots on target. Race to N",
          ""
        ],
        "uk": [
          "Удари в площину. Перший до N",
          ""
        ],
        "es": [
          "Удары в створ. Primero en llegar a N",
          ""
        ],
        "pt": [
          "Chutes ao gol. Corrida para N",
          ""
        ],
        "fr": [
          "Удары в створ. Race to N",
          ""
        ],
        "ro": [
          "Șuturi în poartă. Cursa la N",
          ""
        ],
        "kk": [
          "Тұстамаға соғылған доптар. Біріншісі N дейін",
          ""
        ],
        "en-ca": [
          "Shots on target. Race to N",
          ""
        ],
        "fr-ca": [
          "Shots on target. Race to N",
          ""
        ],
        "sb_ru": [
          "Удары в створ. Первый до N",
          ""
        ],
        "sb_en": [
          "Shots on target. Race to N",
          ""
        ],
        "sb_uk": [
          "Удари в площину. Перший до N",
          ""
        ],
        "bn": [
          "টার্গেটে শট. N পর্যন্ত রেস",
          ""
        ],
        "hi": [
          "Удары в створ. एन (N) तक रेस",
          ""
        ],
        "vi": [
          "Sút trúng mục tiêu. Đua đến N",
          ""
        ],
        "th": [
          "ยิงเข้าเป้า. คนแรกที่ N",
          ""
        ],
        "ms": [
          "Tembakan tepat. Perlumbaan ke N",
          ""
        ],
        "zh": [
          "射正. 赛至 N",
          ""
        ],
        "fa": [
          "شوت در چارچوب. رسیدن به N",
          ""
        ],
        "ru-uz": [
          "Удары в створ. Первый до 3",
          ""
        ],
        "uz": [
          "Удары в створ. Birinchi gacha 3",
          ""
        ],
        "en_ng": [
          "Shots on target. Race to N",
          ""
        ],
        "en_tz": [
          "Shots on target. Race to N",
          ""
        ],
        "en_gh": [
          "Shots on target. Race to N",
          ""
        ]
      },
      "text": {
        "ru": [
          "3: {Team1}"
        ],
        "en": [
          "3: {Team1}"
        ],
        "uk": [
          "3: {Team1}"
        ],
        "es": [
          ""
        ],
        "pt": [
          "3: {Team1}"
        ],
        "fr": [
          ""
        ],
        "ro": [
          "3: {Team1}"
        ],
        "kk": [
          "3: {Team1}"
        ],
        "en-ca": [
          "3: {Team1}"
        ],
        "fr-ca": [
          "3: {Team1}"
        ],
        "sb_ru": [
          "3: П1"
        ],
        "sb_en": [
          "3: 1"
        ],
        "sb_uk": [
          "3: П1"
        ],
        "bn": [
          "3: {Team1}"
        ],
        "hi": [
          "3: {Team1}"
        ],
        "vi": [
          "3: {Team1}"
        ],
        "th": [
          "3: {Team1}"
        ],
        "ms": [
          "3: {Team1}"
        ],
        "zh": [
          "3: {Team1}"
        ],
        "fa": [
          "3: {Team1}"
        ],
        "uz": [
          "3: {Team1}"
        ],
        "en_ng": [
          "3: {Team1}"
        ],
        "en_tz": [
          "3: {Team1}"
        ],
        "en_gh": [
          "3: {Team1}"
        ]
      },
      "textShort": {
        "ru": [
          "3: П1"
        ],
        "en": [
          "3: 1"
        ],
        "uk": [
          "3: П1"
        ],
        "es": [
          ""
        ],
        "pt": [
          "3: 1"
        ],
        "fr": [
          ""
        ],
        "ro": [
          "3: 1"
        ],
        "kk": [
          "3: П1"
        ],
        "en-ca": [
          "3: 1"
        ],
        "fr-ca": [
          "3: 1"
        ],
        "sb_ru": [
          "3: П1"
        ],
        "sb_en": [
          "3: 1"
        ],
        "sb_uk": [
          "3: П1"
        ],
        "bn": [
          "3: 1"
        ],
        "vi": [
          "3: {Team1}"
        ],
        "th": [
          "3: 1"
        ],
        "ms": [
          "3: 1"
        ],
        "zh": [
          "3: 1"
        ],
        "fa": [
          "3: 1"
        ]
      },
      "competitor": {
        "ru": [],
        "en": [],
        "uk": [],
        "es": [],
        "pt": [],
        "fr": [],
        "ro": [],
        "kk": [],
        "en-ca": [],
        "fr-ca": [],
        "sb_ru": [],
        "sb_en": [],
        "sb_uk": [],
        "bn": [],
        "hi": [],
        "vi": [],
        "th": [],
        "ms": [],
        "zh": [],
        "fa": [],
        "ru-uz": [],
        "uz": [],
        "en_ng": [],
        "en_tz": [],
        "en_gh": []
      }
    },
    "isTranslated": false
  },
  {
    "key": "Basketball_[145,[],[0],1,3,[]]",
    "item": {
      "key": null,
      "market": {
        "ru": [
          "Победа с учетом овертайма",
          ""
        ],
        "en": [
          "To win including overtime",
          ""
        ],
        "uk": [
          "Перемога з урахуванням овертайму",
          ""
        ],
        "es": [
          "Ganador (incl. prórroga)",
          ""
        ],
        "pt": [
          "A vencer incluindo o tempo extra",
          ""
        ],
        "fr": [
          "To win including overtime",
          ""
        ],
        "ro": [
          "Victorie inclusiv cu prelungiri",
          ""
        ],
        "kk": [
          "Овертайм ескерілген жеңіс",
          ""
        ],
        "en-ca": [
          "To win including overtime",
          ""
        ],
        "fr-ca": [
          "To win including overtime",
          ""
        ],
        "sb_ru": [
          "Победа с ОТ",
          ""
        ],
        "sb_en": [
          "To win including overtime",
          ""
        ],
        "sb_uk": [
          "Перемога з урахуванням овертайму",
          ""
        ],
        "bn": [
          "ওভারটাইমসহ জিততে",
          ""
        ],
        "hi": [
          "ओवरटाइम मिलाकर जीतना",
          ""
        ],
        "vi": [
          "Thắng, bao gồm hiệp phụ",
          ""
        ],
        "th": [
          "ชนะรวมช่วงทดเวลา",
          ""
        ],
        "ms": [
          "Untuk menang termasuk kerja lebih masa",
          ""
        ],
        "zh": [
          "含加时获胜",
          ""
        ],
        "fa": [
          "برنده با احتساب وقت اضافه",
          ""
        ],
        "ru-uz": [
          "Победа с учетом овертайма",
          ""
        ],
        "uz": [
          "Qo'shimcha taymdagi g'alaba",
          ""
        ],
        "en_ng": [
          "To win including overtime",
          ""
        ],
        "en_tz": [
          "To win including overtime",
          ""
        ],
        "en_gh": [
          "To win including overtime",
          ""
        ]
      },
      "text": {
        "ru": [
          "{Team2}"
        ],
        "en": [
          "{Team2}"
        ],
        "uk": [
          "{Team2}"
        ],
        "es": [
          "{Team2}"
        ],
        "pt": [
          "{Team2}"
        ],
        "fr": [
          ""
        ],
        "ro": [
          "{Team2}"
        ],
        "kk": [
          "{Team2}"
        ],
        "en-ca": [
          "{Team2}"
        ],
        "fr-ca": [
          "{Team2}"
        ],
        "sb_ru": [
          "П2"
        ],
        "sb_en": [
          "2"
        ],
        "sb_uk": [
          "П2"
        ],
        "bn": [
          "{Team2}"
        ],
        "hi": [
          "{टीम 2}"
        ],
        "vi": [
          "{Team2}"
        ],
        "th": [
          "{Team2}"
        ],
        "ms": [
          "{Team2}"
        ],
        "zh": [
          "{Team2}"
        ],
        "fa": [
          "{Team2}"
        ],
        "uz": [
          "{Team2}"
        ],
        "en_ng": [
          "{Team2}"
        ],
        "en_tz": [
          "{Team2}"
        ],
        "en_gh": [
          "{Team2}"
        ]
      },
      "textShort": {
        "ru": [
          "П2"
        ],
        "en": [
          "2"
        ],
        "uk": [
          "П2"
        ],
        "es": [
          ""
        ],
        "pt": [
          "2"
        ],
        "fr": [
          ""
        ],
        "ro": [
          "2"
        ],
        "kk": [
          "П2"
        ],
        "en-ca": [
          "2"
        ],
        "fr-ca": [
          "2"
        ],
        "sb_ru": [
          "П2"
        ],
        "sb_en": [
          "2"
        ],
        "sb_uk": [
          "П2"
        ],
        "bn": [
          "2"
        ],
        "vi": [
          "{Team2}"
        ],
        "th": [
          "2"
        ],
        "ms": [
          "2"
        ],
        "zh": [
          "2"
        ],
        "fa": [
          "2"
        ]
      },
      "competitor": {
        "ru": [],
        "en": [],
        "uk": [],
        "es": [],
        "pt": [],
        "fr": [],
        "ro": [],
        "kk": [],
        "en-ca": [],
        "fr-ca": [],
        "sb_ru": [],
        "sb_en": [],
        "sb_uk": [],
        "bn": [],
        "hi": [],
        "vi": [],
        "th": [],
        "ms": [],
        "zh": [],
        "fa": [],
        "ru-uz": [],
        "uz": [],
        "en_ng": [],
        "en_tz": [],
        "en_gh": []
      }
    },
    "isTranslated": false
  }
]
```
