# Postman HW_1

**Задание. Создать запросы в Postman.** 

|       1       |       2       |
|:---------------:|:---------------:|
| Protocol      | http          |
| IP            | 162.55.220.72 |
| Port          | 5005          |

Создать окружение "Test environment" и внести переменные:
|Variable|Initial value |
|:---------------:|:---------------:|
|url| http://162.55.220.72:5005|
|name|Aleksei |
|age | 29|
|salary|1000 |
|weight|70 |

*Задание 1. EP_1*  
*Method: GET  
EndPoint: /get_method  
request url params:  
name: str  
age: int*

Response:

```json
[
    "Str",
    "Str"
]
```

`Решение`⮯

1. Создать коллекцию с именем "HW_1"
2. Создать запрос с именем "EP_1" и параматерами:
+ Метод "GET" 
+ URL "{{url}}/get_method"
+ Params:
    + KEY = name, VALUE = {{name}}
    + KEY = age, VALUE = {{age}}
4. Нажать "Save" и "Send"

`Результат`⮯

Status 200 OK

```js
[
    "Aleksei",
    "29"
]
```

---

*Задание 2. EP_2*  
*Method: POST  
EndPoint: /user_info_3  
request form data:  
name: str  
age: int  
salary: int*

Response:

```js
{
'name': name,
'age': age,
'salary': salary,
'family': {'children': [['Alex', 24], ['Kate', 12]],
'u_salary_1_5_year': salary * 4}
}
```

`Решение`⮯

1. Создать запрос с именем "EP_2" и параматерами:
+ Метод "POST" 
+ URL "{{url}}/user_info_3"
+ Body/form-data:
    + KEY = name, VALUE = {{name}}
    + KEY = age, VALUE = {{age}}
    + KEY = salary, VALUE = {{salary}}
2. Нажать "Save" и "Send"

`Результат`⮯

Status 200 OK

```json
{
    "age": "29",
    "family": {
        "children": [
            [
                "Alex",
                24
            ],
            [
                "Kate",
                12
            ]
        ],
        "u_salary_1_5_year": 4000
    },
    "name": "Aleksei",
    "salary": 1000
}
```

---

*Задание 3. EP_3*  
*Method: GET  
EndPoint: /object_info_1  
request url params:  
name: str  
age: int  
weight: int*

Response:

```js
{
'name': name,
'age': age,
'daily_food': weight * 0.012,
'daily_sleep': weight * 2.5
}
```

`Решение`⮯

1. Создать запрос с именем "EP_3" и параматерами:
+ Метод "GET" 
+ URL "{{url}}/object_info_1"
+ Params:
    + KEY = name, VALUE = {{name}}
    + KEY = age, VALUE = {{age}}
    + KEY = weight, VALUE = {{weight}}
2. Нажать "Save" и "Send"

`Результат`⮯

Status 200 OK

```json
{
    "age": 29,
    "daily_food": 0.84,
    "daily_sleep": 175.0,
    "name": "Aleksei"
}
```

---

*Задание 4. EP_4*  
*Method: GET  
EndPoint: /object_info_2  
request url params:  
name: str  
age: int  
salary: int*

Response:

```js
{
'start_qa_salary': salary,
'qa_salary_after_6_months': salary * 2,
'qa_salary_after_12_months': salary * 2.7,
'qa_salary_after_1.5_year': salary * 3.3,
'qa_salary_after_3.5_years': salary * 3.8,
'person': {'u_name': [user_name, salary, age],
'u_age': age,
'u_salary_5_years': salary * 4.2}
}
```

`Решение`⮯

1. Создать запрос с именем "EP_4" и параматерами:
+ Метод "GET" 
+ URL "{{url}}/object_info_2"
+ Params:
    + KEY = name, VALUE = {{name}}
    + KEY = age, VALUE = {{age}}
    + KEY = salary, VALUE = {{salary}}
2. Нажать "Save" и "Send"

`Результат`⮯

Status 200 OK

```json
{
    "person": {
        "u_age": 29,
        "u_name": [
            "Aleksei",
            1000,
            29
        ],
        "u_salary_5_years": 4200.0
    },
    "qa_salary_after_1.5_year": 3300.0,
    "qa_salary_after_12_months": 2700.0,
    "qa_salary_after_3.5_years": 3800.0,
    "qa_salary_after_6_months": 2000,
    "start_qa_salary": 1000
}
```

---

*Задание 5. EP_5*  
*Method: GET  
EndPoint: /object_info_3  
request url params:  
name: str  
age: int  
salary: int*

Response:

```js
{
'name': name,
'age': age,
'salary': salary,
'family': {'children': [['Alex', 24], ['Kate', 12]],
'pets': {'cat':{'name':'Sunny','age': 3},'dog':{'name':'Luky','age': 4}},
'u_salary_1_5_year': salary * 4}
}
```

`Решение`⮯

1. Создать запрос с именем "EP_5" и параматерами:
+ Метод "GET" 
+ URL "{{url}}/object_info_3"
+ Params:
    + KEY = name, VALUE = {{name}}
    + KEY = age, VALUE = {{age}}
    + KEY = salary, VALUE = {{salary}}
2. Нажать "Save" и "Send"

`Результат`⮯

Status 200 OK

```json
{
    "age": "29",
    "family": {
        "children": [
            [
                "Alex",
                24
            ],
            [
                "Kate",
                12
            ]
        ],
        "pets": {
            "cat": {
                "age": 3,
                "name": "Sunny"
            },
            "dog": {
                "age": 4,
                "name": "Luky"
            }
        },
        "u_salary_1_5_year": 4000
    },
    "name": "Aleksei",
    "salary": 1000
}
```

---

*Задание 6. EP_6*  
*Method: GET  
EndPoint: /object_info_4  
request url params:  
name: str  
age: int  
salary: int*

Response:

```js
{
'name': name,
'age': int(age),
'salary': [salary, str(salary * 2), str(salary * 3)]
}
```

`Решение`⮯

1. Создать запрос с именем "EP_6" и параматерами:
+ Метод "GET" 
+ URL "{{url}}/object_info_4"
+ Params:
    + KEY = name, VALUE = {{name}}
    + KEY = age, VALUE = {{age}}
    + KEY = salary, VALUE = {{salary}}
2. Нажать "Save" и "Send"

`Результат`⮯

Status 200 OK

```json
{
    "age": 29,
    "name": "Aleksei",
    "salary": [
        1000,
        "2000",
        "3000"
    ]
}
```

---

*Задание 7. EP_7*  
*Method: POST  
EndPoint: /user_info_2    
request form data:   
name: str  
age: int  
salary: int*

Response:

```js
{
'start_qa_salary': salary,
'qa_salary_after_6_months': salary * 2,
'qa_salary_after_12_months': salary * 2.7,
'qa_salary_after_1.5_year': salary * 3.3,
'qa_salary_after_3.5_years': salary * 3.8,
'person': {'u_name': [user_name, salary, age],
'u_age': age,
'u_salary_5_years': salary * 4.2}
}
```

`Решение`⮯

1. Создать запрос с именем "EP_7" и параматерами:
+ Метод "POST" 
+ URL "{{url}}/user_info_2"
+ Body/form-data:
    + KEY = name, VALUE = {{name}}
    + KEY = age, VALUE = {{age}}
    + KEY = salary, VALUE = {{salary}}
2. Нажать "Save" и "Send"

`Результат`⮯

Status 200 OK

```json
{
    "person": {
        "u_age": 29,
        "u_name": [
            "Aleksei",
            1000,
            29
        ],
        "u_salary_5_years": 4200.0
    },
    "qa_salary_after_1.5_year": 3300.0,
    "qa_salary_after_12_months": 2700.0,
    "qa_salary_after_3.5_years": 3800.0,
    "qa_salary_after_6_months": 2000,
    "start_qa_salary": 1000
}
```

---
