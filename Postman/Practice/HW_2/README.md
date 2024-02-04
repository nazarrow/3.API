# Postman HW_2

*Задание 1. http://162.55.220.72:5005/first*   

`Решение`⮯

Метод GET

1. Отправить запрос:

```
   {{url}}/first
```

2. Статус код 200:

Tests:
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

3. Проверить, что в body приходит правильный string:

```js
pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("This is the first responce from server!ss");
});
```

`Результат`⮯

Status 200 OK

Test results 2/2

---

*Задание 2. http://162.55.220.72:5005/user_info_3*   

`Решение`⮯

Метод POST  
Body/form-data:  
KEY = name VALUE = {{name}}  
KEY = age VALUE = {{age}}  
KEY = salary VALUE = {{salary}}

1. Отправить запрос:

```
{{url}}/user_info_3
```

2. Статус код 200:

Tests:
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

3. Спарсить response body в json:

```js
let respBody = pm.response.json();
```

4. Проверить, что name в ответе равно name s request (name вбить руками):

```js
pm.test("name resp = name req", function () {
    pm.expect(respBody.name).to.eql("Aleksei");
});
```

5. Проверить, что age в ответе равно age s request (age вбить руками):

```js
pm.test("age resp = age req", function () {
    pm.expect(respBody.age).to.eql("29");
});
```

6. Проверить, что salary в ответе равно salary s request (salary вбить руками):

```js
pm.test("salary resp = salary req", function () {
    pm.expect(respBody.salary).to.eql(1000);
});
```

7. Спарсить request:

```js
let reqData = request.data;
```

8. Проверить, что name в ответе равно name s request (name забрать из request):

```js
pm.test("name resp = name req", function () {
    pm.expect(respBody.name).to.eql(reqData.name);
});
```

9.  Проверить, что age в ответе равно age s request (age забрать из request):

```js
pm.test("age resp = age req", function () {
    pm.expect(respBody.age).to.eql(reqData.age);
});
```

10. Проверить, что salary в ответе равно salary s request (salary забрать из request):

```js
pm.test("salary resp = salary req", function () {
    pm.expect(respBody.salary).to.eql(parseInt(reqData.salary));
});
```

11. Вывести в консоль параметр family из response:

```js
console.log(respBody.family);
```

12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request):

```js
pm.test("resp u_salary_1_5_year = req salary*4", function () {
    pm.expect(respBody.family.u_salary_1_5_year).to.eql(+reqData.salary*4);
});
```

`Результат`⮯

Status 200 OK

Test results 8/8

---

*Задание 3. http://162.55.220.72:5005/object_info_3*   

Метод GET  
Params:  
KEY = name VALUE = {{name}}  
KEY = age VALUE = {{age}}  
KEY = salary VALUE = {{salary}}

`Решение`⮯

1. Отправить запрос:

```
{{url}}/object_info_3
```

2. Статус код 200:

Tests:
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

3. Спарсить response body в json:

```js
let respBody = pm.response.json();
```

4. Спарсить request:

```js
let reqData = pm.request.url.query.toObject();
```

5. Проверить, что name в ответе равно name s request (name забрать из request):

```js
pm.test("name resp = name req", function () {
    pm.expect(respBody.name).to.eql(reqData.name);
});
```

6. Проверить, что age в ответе равно age s request (age забрать из request):

```js
pm.test("age resp = age req", function () {
    pm.expect(respBody.age).to.eql(reqData.age);
});
```

7. Проверить, что salary в ответе равно salary s request (salary забрать из request):

```js
pm.test("salary resp = salary req", function () {
    pm.expect(respBody.salary).to.eql(parseInt(reqData.salary));
});
```

8. Вывести в консоль параметр family из response:

```js
console.log(respBody.family);
```

9.  Проверить, что у параметра dog есть параметры name:

```js
pm.test("resp dog contain name", function () {
    pm.expect(respBody.family.pets.dog).to.have.property("name");
});
```

10. Проверить, что у параметра dog есть параметры age:

```js
pm.test("resp dog contain age", function () {
    pm.expect(respBody.family.pets.dog).to.have.property("age");
});
```

11. Проверить, что параметр name имеет значение Luky:

```js
pm.test("resp name contain Luky", function () {
    pm.expect(respBody.family.pets.dog.name).to.eql("Luky");
});
```

12. Проверить, что параметр age имеет значение 4:

```js
pm.test("resp age contain 4", function () {
    pm.expect(respBody.family.pets.dog.age).to.eql(4);
});
```

`Результат`⮯

Status 200 OK

Test results 8/8

---

*Задание 4. http://162.55.220.72:5005/object_info_4*   

Метод GET  
Params:  
KEY = name VALUE = {{name}}  
KEY = age VALUE = {{age}}  
KEY = salary VALUE = {{salary}}

`Решение`⮯

1. Отправить запрос:

```
{{url}}/object_info_4
```

2. Статус код 200:

Tests:
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

3. Спарсить response body в json:

```js
let respBody = pm.response.json();
```

4. Спарсить request:

```js
let reqData = pm.request.url.query.toObject();
```

5. Проверить, что name в ответе равно name s request (name забрать из request):

```js
pm.test("name resp = name req", function () {
    pm.expect(respBody.name).to.eql(reqData.name);
});
```

6. Проверить, что age в ответе равно age из request (age забрать из request):

```js
pm.test("age resp = age req", function () {
    pm.expect(respBody.age).to.eql(+reqData.age);
});
```

7. Вывести в консоль параметр salary из request:

```js
console.log("Request salary", reqData.salary);
```

8. Вывести в консоль параметр salary из response:

```js
console.log("Reponse salary", respBody.salary);
```

9.  Вывести в консоль 0-й элемент параметра salary из response:

```js
console.log(respBody.salary[0]);
```

10.  Вывести в консоль 1-й элемент параметра salary параметр salary из response:

```js
console.log(respBody.salary[1]);
```

11.  Вывести в консоль 2-й элемент параметра salary параметр salary из response:

```js
console.log(respBody.salary[2]);
```

12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request):

```js
pm.test("resp salary [0] = req salary", function () {
    pm.expect(respBody.salary[0]).to.eql(+reqData.salary);
});
```

13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request):

```js
pm.test("resp salary [1] = req salary*2", function () {
    pm.expect(respBody.salary[1]).to.eql+(reqData.salary*2);
});
```

14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request):

```js
pm.test("resp salary [2] = req salary*2", function () {
    pm.expect(respBody.salary[2]).to.eql+(reqData.salary*3);
});
```
*Использовал переменные и окружение, но решение 15- 20 ниже.*

15. Создать в окружении переменную name:
18. Передать в окружение переменную name:
    
```js
let respBody = pm.request.url.query.toObject()
pm.environment.set(\"name\", respBody.name)
```

16.  Создать в окружении переменную age:
19.  Передать в окружение переменную age:
    
```js
let respBody = pm.request.url.query.toObject()
pm.environment.set(\"age\", respBody.age)
```

17.  Создать в окружении переменную salary:
20.  Передать в окружение переменную salary:
    
```js
let respBody = pm.request.url.query.toObject()
pm.environment.set(\"salary\", respBody.salary)
```

21.  Написать цикл который выведет в консоль по порядку элементы списка из параметра salary:

```js
for (let i of respBody.salary) {
     console.log(i);
};
```

`Результат`⮯

Status 200 OK

Test results 6/6

---

*Задание 5. http://162.55.220.72:5005/user_info_2*   

Метод POST  
Body/form-data:  
KEY = name VALUE = {{name}}  
KEY = age VALUE = {{age}}  
KEY = salary VALUE = {{salary}}

`Решение`⮯

1. Вставить параметр salary из окружения в request:
2. Вставить параметр age из окружения в age:
3. Вставить параметр name из окружения в name:
4. Отправить запрос:

```js
{{url}}/user_info_2
```

5. Статус код 200:

Tests:
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

6. Спарсить response body в json:

```js
let respBody = pm.response.json();
```

7. Спарсить request:

```js
let reqData = request.data;
```

8. Проверить, что json response имеет параметр start_qa_salary:

```js
pm.test("resp json contains start_qa_salary", function () {
    pm.expect(respBody).to.have.property("start_qa_salary");
});
```

9.  Проверить, что json response имеет параметр qa_salary_after_6_months:

```js
pm.test("resp json contains qa_salary_after_6_months", function () {
    pm.expect(respBody).to.have.property("qa_salary_after_6_months");
});
```

10. Проверить, что json response имеет параметр qa_salary_after_12_months:

```js
pm.test("resp json contains qa_salary_after_12_months", function () {
    pm.expect(respBody).to.have.property("qa_salary_after_12_months");
});
```

11. Проверить, что json response имеет параметр qa_salary_after_1.5_year:

```js
pm.test("resp json contains qa_salary_after_1.5_year", function () {
    pm.expect(respBody).to.have.property("qa_salary_after_1.5_year");
});
```

12. Проверить, что json response имеет параметр qa_salary_after_3.5_years:

```js
pm.test("resp json contains qa_salary_after_3.5_years", function () {
    pm.expect(respBody).to.have.property("qa_salary_after_3.5_years");
});
```

13. Проверить, что json response имеет параметр person:

```js
pm.test("resp json contains person", function () {
    pm.expect(respBody).to.have.property("person");
});
```

14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request):

```js
pm.test("resp start_qa_salary = req start_qa_salary", function () {
    pm.expect(respBody.start_qa_salary).to.eql(+reqData.salary);
});
```

15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request):

```js
pm.test("resp qa_salary_after_6_months = req salary*2", function () {
    pm.expect(respBody.qa_salary_after_6_months).to.eql(+reqData.salary*2);
});
```

16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request):

```js
pm.test("resp qa_salary_after_12_months = req salary*2.7", function () {
    pm.expect(respBody.qa_salary_after_12_months).to.eql(+reqData.salary*2.7);
});
```

17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request):

```js
pm.test("resp qa_salary_after_1.5_year = req salary*3.3", function () {
    pm.expect(respBody["qa_salary_after_1.5_year"]).to.eql(+reqData.salary*3.3);
});
```

18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request):

```js
pm.test("resp qa_salary_after_3.5_years = req salary*3.8", function () {
    pm.expect(respBody["qa_salary_after_3.5_years"]).to.eql(+reqData.salary*3.8);
});
```

19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request):

```js
pm.test("resp person [1] u_name = req salary", function () {
    pm.expect(respBody.person.u_name[1]).to.eql(+reqData.salary);
});
```

20. Проверить, что что параметр u_age равен age из request (age забрать из request):

```js
pm.test("resp u_age = req age", function () {
    pm.expect(respBody.person.u_age).to.eql(+reqData.age);
});
```

21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request):

```js
pm.test("resp u_salary_5_years  = req salary*4.2", function () {
    pm.expect(respBody.person.u_salary_5_years).to.eql(+reqData.salary*4.2);
});
```

22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person:

```js
for (let i = 0; i < respBody.person.u_name.length; i++) {
  console.log("Вывод из списка, элемента с индексом" + i + ": " + respBody.person.u_name[i]);
}
// либо 
/*
for (let i of respBody.person.u_name){
    console.log(i)
}
*/
// либо 
/*
for(let KEY in respBody.person) {
   if(typeof(respBody.person[KEY]) == "object"){
       for(let i = 0; i < Object.keys(respBody.person[KEY]).length; i++){
           console.log(respBody.person[KEY][i]);
       }
   }
   else if(typeof(respBody.person[KEY]) != "object") {
        console.log(respBody.person[KEY]);
   }
}
*/
```

`Результат`⮯

Status 200 OK

Test results 15/15







