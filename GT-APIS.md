# GT APIs definition

- [Translation APIs](#translation-apis)

## Translation API
Body of request: Array of selection keys in format "Sport_OutcomeSelectionKey" - for example:
- ["F_[14,[3],[0],66,11,[]]"]
- ["F_[14,[3],[0],66,11,[]]", "F_[2,[],[0],1,3,[]]"]

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
curl -X POST https://public-api-stage-hz.betgate.dev/apt/gt/translate/selections/en -H "Content-Type: application/json" -H "X-Api-Key: 6b4314aa-638b-4f8b-a0eb-d17f830fc32a" "[\"F_[14,[3],[0],66,11,[]]\",\"B_[145,[],[0],1,3,[]]\"]"
```
```json
[
  {
    "key": "F_[14,[3],[0],66,11,[]]",
    "item": {
      "market": {
        "en": [
          "Shots on target. Race to N",
          ""
        ]
      },
      "text": {
        "en": [
          "3: {Team1}"
        ]
      },
      "competitor": {},
      "textShort": {
        "en": [
          "3: 1"
        ]
      }
    },
    "isTranslated": false
  },
  {
    "key": "B_[145,[],[0],1,3,[]]",
    "item": {
      "market": {
        "en": [
          "To win including overtime",
          ""
        ]
      },
      "text": {
        "en": [
          "{Team2}"
        ]
      },
      "competitor": {},
      "textShort": {
        "en": [
          "2"
        ]
      }
    },
    "isTranslated": false
  }
]
```

### POST /api/translate/selections
Retrieve translations for all languages.

```
curl -X POST https://public-api-stage-hz.betgate.dev/apt/gt/translate/selections -H "Content-Type: application/json" -H "X-Api-Key: 6b4314aa-638b-4f8b-a0eb-d17f830fc32a" "[\"F_[14,[3],[0],66,11,[]]\",\"B_[145,[],[0],1,3,[]]\"]"
```
```json
[
  {
    "key": "F_[14,[3],[0],66,11,[]]",
    "item": {
      "market": {
        "bn": [
          "টার্গেটে শট. N পর্যন্ত রেস",
          ""
        ],
        "en": [
          "Shots on target. Race to N",
          ""
        ],
        "es": [
          "Disparos a puerta. Primero en llegar a N",
          ""
        ],
        "fa": [
          "شوت در چارچوب. رسیدن به N",
          ""
        ],
        "fr": [
          "Tirs cadrés. Premier à N",
          ""
        ],
        "hi": [
          "टारगेट. एन (N) तक रेस",
          ""
        ],
        "kk": [
          "Қақпаға бағытталған соққы. Біріншісі N дейін",
          ""
        ],
        "ms": [
          "Tembakan tepat. Perlumbaan ke N",
          ""
        ],
        "pt": [
          "Chutes no gol. Primeiro a chegar №.",
          ""
        ],
        "ro": [
          "Lovituri la poartă. Cursa la N",
          ""
        ],
        "ru": [
          "Удары в створ. Первый до N",
          ""
        ],
        "th": [
          "ยิงเข้าเป้า. คนแรกที่ N",
          ""
        ],
        "uk": [
          "Удари в площину. Перший до N",
          ""
        ],
        "uz": [
          "Удары в створ. Birinchi gacha 3",
          ""
        ],
        "vi": [
          "Sút trúng mục tiêu. Đua đến N",
          ""
        ],
        "zh": [
          "射正. 赛至 N",
          ""
        ],
        "en-ca": [
          "Shots on target. Race to N",
          ""
        ],
        "en_gh": [
          "Shots on target. Race to N",
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
        "fr-ca": [
          "Tirs cadrés. Premier à N",
          ""
        ],
        "ru-uz": [
          "Удары в створ. Первый до 3",
          ""
        ],
        "sb_en": [
          "Shots on target. Race to N",
          ""
        ],
        "sb_ru": [
          "Удары в створ. Первый до N",
          ""
        ],
        "sb_uk": [
          "Удари в площину. Перший до N",
          ""
        ]
      },
      "text": {
        "bn": [
          "3: {Team1}"
        ],
        "en": [
          "3: {Team1}"
        ],
        "es": [
          "3: {Team1}"
        ],
        "fa": [
          "3: {Team1}"
        ],
        "fr": [
          "3: {Team1}"
        ],
        "hi": [
          "3: {Team1}"
        ],
        "kk": [
          "3: {Team1}"
        ],
        "ms": [
          "3: {Team1}"
        ],
        "pt": [
          "3: {Team1}"
        ],
        "ro": [
          "3: {Team1}"
        ],
        "ru": [
          "3: {Team1}"
        ],
        "th": [
          "3: {Team1}"
        ],
        "uk": [
          "3: {Team1}"
        ],
        "uz": [
          "3: {Team1}"
        ],
        "vi": [
          "3: {Team1}"
        ],
        "zh": [
          "3: {Team1}"
        ],
        "en-ca": [
          "3: {Team1}"
        ],
        "en_gh": [
          ""
        ],
        "en_ng": [
          ""
        ],
        "en_tz": [
          ""
        ],
        "fr-ca": [
          "3: {Team1}"
        ],
        "sb_en": [
          "3: 1"
        ],
        "sb_ru": [
          "3: П1"
        ],
        "sb_uk": [
          "3: П1"
        ]
      },
      "competitor": {
        "bn": [],
        "en": [],
        "es": [],
        "fa": [],
        "fr": [],
        "hi": [],
        "kk": [],
        "ms": [],
        "pt": [],
        "ro": [],
        "ru": [],
        "th": [],
        "uk": [],
        "uz": [],
        "vi": [],
        "zh": [],
        "en-ca": [],
        "en_gh": [],
        "en_ng": [],
        "en_tz": [],
        "fr-ca": [],
        "ru-uz": [],
        "sb_en": [],
        "sb_ru": [],
        "sb_uk": []
      },
      "textShort": {
        "bn": [
          "3: 1"
        ],
        "en": [
          "3: 1"
        ],
        "es": [
          "3: 1"
        ],
        "fa": [
          "3: 1"
        ],
        "fr": [
          "3: 1"
        ],
        "kk": [
          "3: П1"
        ],
        "ms": [
          "3: 1"
        ],
        "pt": [
          "3: 1"
        ],
        "ro": [
          "3: 1"
        ],
        "ru": [
          "3: П1"
        ],
        "th": [
          "3: 1"
        ],
        "uk": [
          "3: П1"
        ],
        "vi": [
          "3: {Team1}"
        ],
        "zh": [
          "3: 1"
        ],
        "en-ca": [
          "3: 1"
        ],
        "fr-ca": [
          "3: 1"
        ],
        "sb_en": [
          "3: 1"
        ],
        "sb_ru": [
          "3: П1"
        ],
        "sb_uk": [
          "3: П1"
        ]
      }
    },
    "isTranslated": false
  },
  {
    "key": "B_[145,[],[0],1,3,[]]",
    "item": {
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
          "Vencedor (incl. prolongamento)",
          ""
        ],
        "fr": [
          "Gagner (incluent les prolongations)",
          ""
        ],
        "ro": [
          "Pentru a câștiga inclusiv prelungiri",
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
          "Gagner (incluent les prolongations)",
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
          "{Team2}"
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
          "{Team2}"
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
          ""
        ],
        "en_tz": [
          ""
        ],
        "en_gh": [
          ""
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
          "2"
        ],
        "pt": [
          "2"
        ],
        "fr": [
          "2"
        ],
        "ro": [
          "2"
        ],
        "kk": [
          "П2"
        ],
        "en-ca": [
          "1"
        ],
        "fr-ca": [
          "1"
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
      }
    },
    "isTranslated": false
  }
]
```
