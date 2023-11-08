# Postman HW_3

*Задание 1. http://162.55.220.72:5005/login*  

`Решение`⮯

1. Необходимо залогиниться:  
Метод POST

```
http://162.55.220.72:5005/login
```

2. Body/form-data:

```
login : Aleksei(str (кроме /))
password : qwerty (str)
```

3. Приходящий токен необходимо передать во все остальные запросы:

```json
{
    "token": "/s34lfgbj/Aleksei/jjd909/25686kjkWpqc4158qwerty319402evny"
}
```

4. Дальше все запросы требуют наличие токена:

```
Создать окружение с имененем "Token environment".
Параметры:  
KEY = name VALUE = Aleksei
KEY = age VALUE = 29
KEY = salary VALUE = 1000
KEY = auth_token VALUE = /s34lfgbj/Aleksei/jjd909/25686kjkWpqc4158qwerty319402evny    
```

---

*Задание 2. http://162.55.220.72:5005/user_info*  

Request (RAW JSON):  

POST  
age: int  
salary: int  
name: str  
auth_token  


Response:

```
{'start_qa_salary':salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
                                'u_age':age,
                                'u_salary_1.5_year': salary * 4}
                                }
```

`Решение`⮯

RAW JSON:
```
{
    "age" : "{{age}}",
    "name" : "{{name}}",
    "salary" : "{{salary}}",
    "auth_token" : "{{auth_token}}"
}
```

Tests:
1. Статус код 200:

```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

2. Проверка структуры json в ответе:

Используем [jsonschema.net](https://www.jsonschema.net/app/schemas/184821)

```js
let schema = {
    "$schema": "https://json-schema.org/draft/2019-09/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "default": {},
    "title": "Root Schema",
    "required": [
        "person",
        "qa_salary_after_12_months",
        "qa_salary_after_6_months",
        "start_qa_salary"
    ],
    "properties": {
        "person": {
            "type": "object",
            "default": {},
            "title": "The person Schema",
            "required": [
                "u_age",
                "u_name",
                "u_salary_1_5_year"
            ],
            "properties": {
                "u_age": {
                    "type": "integer",
                    "default": 0,
                    "title": "The u_age Schema",
                    "examples": [
                        29
                    ]
                },
                "u_name": {
                    "type": "array",
                    "default": [],
                    "title": "The u_name Schema",
                    "items": {
                        "anyOf": [{
                            "type": "string",
                            "default": "",
                            "title": "A Schema",
                            "examples": [
                                "Aleksei"
                            ]
                        },
                        {
                            "type": "integer",
                            "title": "A Schema",
                            "examples": [
                                1000,
                                29
                            ]
                        }]
                    },
                    "examples": [
                        ["Aleksei",
                            1000,
                            29
                        ]
                    ]
                },
                "u_salary_1_5_year": {
                    "type": "integer",
                    "default": 0,
                    "title": "The u_salary_1_5_year Schema",
                    "examples": [
                        4000
                    ]
                }
            },
            "examples": [{
                "u_age": 29,
                "u_name": [
                    "Aleksei",
                    1000,
                    29
                ],
                "u_salary_1_5_year": 4000
            }]
        },
        "qa_salary_after_12_months": {
            "type": "number",
            "default": 0.0,
            "title": "The qa_salary_after_12_months Schema",
            "examples": [
                2900.0
            ]
        },
        "qa_salary_after_6_months": {
            "type": "integer",
            "default": 0,
            "title": "The qa_salary_after_6_months Schema",
            "examples": [
                2000
            ]
        },
        "start_qa_salary": {
            "type": "integer",
            "default": 0,
            "title": "The start_qa_salary Schema",
            "examples": [
                1000
            ]
        }
    },
    "examples": [{
        "person": {
            "u_age": 29,
            "u_name": [
                "Aleksei",
                1000,
                29
            ],
            "u_salary_1_5_year": 4000
        },
        "qa_salary_after_12_months": 2900.0,
        "qa_salary_after_6_months": 2000,
        "start_qa_salary": 1000
    }]
};
   
let result = tv4.validateResult(pm.response.json(), schema);
pm.test('Schema is valid', function () {
    pm.expect(result.valid).to.be.true;
});
```

3. В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент:

```js
let respData = pm.response.json();
let reqData = JSON.parse(request.data);

pm.test("start_qa_salary = 1000", function () {
    pm.expect(respData.start_qa_salary).to.eql+(reqData.salary);
});

pm.test("qa_salary_after_6_months *2 = 2000", function () {
    pm.expect(respData.qa_salary_after_6_months).to.eql+(reqData.salary*2);
});

pm.test("qa_salary_after_12_months *2.9 = 2900", function () {
    pm.expect(respData.qa_salary_after_12_months).to.eql+(reqData.salary*2.9);
});

pm.test("u_salary_1_5_year *4 = 4000", function () {
    pm.expect(respData.person.u_salary_1_5_year).to.eql+(reqData.salary*4);
});

```

4. Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса
http://162.55.220.72:5005/get_test_user:

```js
pm.environment.set("new_salary", respData.person.u_salary_1_5_year);
console.log("u_salary_1_5_year", respData.person.u_salary_1_5_year);
```

---

*Задание 3. http://162.55.220.72:5005/new_data*  

Request:  

POST  
age: int  
salary: int  
name: str  
auth_token  

Response:

```
{
'name':name,
'age': int(age),
'salary': [salary, str(salary*2), str(salary*3)]
}
```

`Решение`⮯

Tests:
1. Статус код 200:

```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

2. Проверка структуры json в ответе:

```js
let schema = {
    "$schema": "https://json-schema.org/draft/2019-09/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "default": {},
    "title": "Root Schema",
    "required": [
        "age",
        "name",
        "salary"
    ],
    "properties": {
        "age": {
            "type": "integer",
            "default": 0,
            "title": "The age Schema",
            "examples": [
                29
            ]
        },
        "name": {
            "type": "string",
            "default": "",
            "title": "The name Schema",
            "examples": [
                "Aleksei"
            ]
        },
        "salary": {
            "type": "array",
            "default": [],
            "title": "The salary Schema",
            "items": {
                "anyOf": [{
                    "type": "integer",
                    "default": 0,
                    "title": "A Schema",
                    "examples": [
                        1000
                    ]
                },
                {
                    "type": "string",
                    "title": "A Schema",
                    "examples": [
                        "2000",
                        "3000"
                    ]
                }]
            },
            "examples": [
                [1000,
                    "2000",
                    "3000"
                ]
            ]
        }
    },
    "examples": [{
        "age": 29,
        "name": "Aleksei",
        "salary": [
            1000,
            "2000",
            "3000"
        ]
    }]
};

let result = tv4.validateResult(pm.response.json(), schema);

pm.test('Schema is valid', function () {
    pm.expect(result.valid).to.be.true;
    });
```

3. В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент:

```js
let respData = pm.response.json();
let reqData = request.data;

pm.test("resp salary[0] = req salary*1", function () {
    pm.expect(respData.salary[0]).to.eql+(reqData.salary);
});

pm.test("resp salary[1] = req salary*2", function () {
    pm.expect(respData.salary[1]).to.eql+(reqData.salary[1]);
});

pm.test("resp salary[2] = req salary*3", function () {
    pm.expect(respData.salary[2]).to.eql+(reqData.salary*2);
});
```

4. Проверить, что 2-й элемент массива salary больше 1-го и 0-го:

```js
pm.test("resp salary[2] > resp salary[1] and > resp salary[0]", function () {
    pm.expect(+respData.salary[2]).to.above(+respData.salary[1]);
    pm.expect(+respData.salary[1]).to.above(respData.salary[0]);
});
```

---

*Задание 4. http://162.55.220.72:5005/test_pet_info*  

Request:  

POST
age: int
weight: int
name: str
auth_token

Response:

```
{
'name': name,
'age': age,
'daily_food':weight * 0.012,
'daily_sleep': weight * 2.5
}
 ```
 
Tests:

1. Статус код 200:

```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

2. Проверка структуры json в ответе:

```js
let schema = {
    "$schema": "https://json-schema.org/draft/2019-09/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "default": {},
    "title": "Root Schema",
    "required": [
        "age",
        "daily_food",
        "daily_sleep",
        "name"
    ],
    "properties": {
        "age": {
            "type": "integer",
            "default": 0,
            "title": "The age Schema",
            "examples": [
                29
            ]
        },
        "daily_food": {
            "type": "number",
            "default": 0.0,
            "title": "The daily_food Schema",
            "examples": [
                0.84
            ]
        },
        "daily_sleep": {
            "type": "number",
            "default": 0.0,
            "title": "The daily_sleep Schema",
            "examples": [
                175.0
            ]
        },
        "name": {
            "type": "string",
            "default": "",
            "title": "The name Schema",
            "examples": [
                "Aleksei"
            ]
        }
    },
    "examples": [{
        "age": 29,
        "daily_food": 0.84,
        "daily_sleep": 175.0,
        "name": "Aleksei"
    }]
};

let result = tv4.validateResult(pm.response.json(), schema);

pm.test('Schema is valid', function () {
    pm.expect(result.valid).to.be.true;
});
```

3. В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент:

```js
let respWeight = pm.response.json();
let reqWeight = request.data;

pm.test("resp daily_food = req weight*0.012", function () {
       pm.expect(respWeight.daily_food).to.eql(reqWeight.weight*0.012);
});

pm.test("resp daily_sleep = req weight*2.5", function () {
       pm.expect(respWeight.daily_sleep).to.eql(reqWeight.weight*2.5);
});
```

---

*Задание 5. http://162.55.220.72:5005/get_test_user*  

Request:

POST  
age: int  
salary: int  
name: str  
auth_token  

Response:

```
{
'name': name,
'age':age,
'salary': salary,
'family':{'children':[['Alex', 24],['Kate', 12]],
'u_salary_1.5_year': salary * 4}
}
```

Tests:

1. Статус код 200:

```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

2. Проверка структуры json в ответе:

```js
let schema = {
    "$schema": "https://json-schema.org/draft/2019-09/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "default": {},
    "title": "Root Schema",
    "required": [
        "age",
        "family",
        "name",
        "salary"
    ],
    "properties": {
        "age": {
            "type": "string",
            "default": "",
            "title": "The age Schema",
            "examples": [
                "29"
            ]
        },
        "family": {
            "type": "object",
            "default": {},
            "title": "The family Schema",
            "required": [
                "children",
                "u_salary_1_5_year"
            ],
            "properties": {
                "children": {
                    "type": "array",
                    "default": [],
                    "title": "The children Schema",
                    "items": {
                        "type": "array",
                        "title": "A Schema",
                        "items": {
                            "anyOf": [{
                                "type": "string",
                                "title": "A Schema",
                                "examples": [
                                    "Alex",
                                    "Kate"
                                ]
                            },
                            {
                                "type": "integer",
                                "title": "A Schema",
                                "examples": [
                                    24,
                                    12
                                ]
                            }]
                        },
                        "examples": [
                            ["Alex",
                                24
                            ],
                            ["Kate",
                                12
                            ]
                        ]
                    },
                    "examples": [
                        [
                            ["Alex",
                                24
                            ],
                            ["Kate",
                                12
                            ]
                        ]
                    ]
                },
                "u_salary_1_5_year": {
                    "type": "integer",
                    "default": 0,
                    "title": "The u_salary_1_5_year Schema",
                    "examples": [
                        4000
                    ]
                }
            },
            "examples": [{
                "children": [
                    ["Alex",
                        24
                    ],
                    ["Kate",
                        12
                    ]
                ],
                "u_salary_1_5_year": 4000
            }]
        },
        "name": {
            "type": "string",
            "default": "",
            "title": "The name Schema",
            "examples": [
                "Aleksei"
            ]
        },
        "salary": {
            "type": "integer",
            "default": 0,
            "title": "The salary Schema",
            "examples": [
                1000
            ]
        }
    },
    "examples": [{
        "age": "29",
        "family": {
            "children": [
                ["Alex",
                    24
                ],
                ["Kate",
                    12
                ]
            ],
            "u_salary_1_5_year": 4000
        },
        "name": "Aleksei",
        "salary": 1000
    }]
};

let result = tv4.validateResult(pm.response.json(), schema);

pm.test('Schema is valid', function () {
    pm.expect(result.valid).to.be.true;
    });
```

3. Проверить что значение поля name = значению переменной name из окружения:

```js
let resp = pm.response.json();

pm.test("value field name = value name variable from the environment", function () {
    pm.expect(resp.name).to.eql(pm.environment.get("name"));
});
```

4. Проверить что значение поля age в ответе соответсвует отправленному в запросе значению поля age:

```js
let req = request.data;

pm.test("rsp value field age corresponds req value field age", function () {
    pm.expect(resp.age).to.eql(req.age);
});
```

---

