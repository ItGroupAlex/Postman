# QA   
Текстовка заданий Homework 1-3: [HW_exercises](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/HW_exercises.txt "link")   
Homework 1-3 (code): [QA_HW.postman_collection.json](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/QA_HW.postman_collection.json "link")  
Homework 1-3 (result of run): [QA_HW.postman_test_run.json](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/QA_HW.postman_test_run.json "link")   

Homework Charles:   
* [задание и ход выполнения](https://github.com/ItGroupAlex/Postman/blob/main/Charles/Charles_QA_HW.md "link")     
* [выгрузка из Charles](https://github.com/ItGroupAlex/Postman/blob/main/Charles/Charles_HW_export.chls "link")
* [выгрузка из Postman](https://github.com/ItGroupAlex/Postman/blob/main/Charles/Charles.postman_collection.json "link")   

Homework Fiddler:   
* [задание и ход выполнения](https://github.com/ItGroupAlex/Postman/blob/main/Fiddler/Fiddler_QA_HW.md "link")     
* [выгрузка из Fiddler](https://github.com/ItGroupAlex/Postman/blob/main/Fiddler/Rules_HW_fiddler.farx "link")
* [выгрузка из Postman](https://github.com/ItGroupAlex/Postman/blob/main/Fiddler/Fiddler.postman_collection.json "link")    


# Основные команды

**ПАРСИНГ**

// Спарсить response body в json.  

``` js
var jsonData = pm.response.json();
```


// Спарсить request. (POST/GET) (переменные в Body - form-data)  

``` js 
var req = request.data
```


// Спарсить request. (POST/GET) (переменные в Body - raw(JSON))  

``` js
var req = JSON.parse(pm.request.body);
```

//Спарсить request.(GET)  

``` js
var req_url = pm.request.url.query.toObject();
```



//проверка схемы JSON   

``` js
var schema = {
    "type": "object",
    "required": [
        "age",
        "name",
        "salary"
    ],
    "properties": {
        "age": {
            "type": "integer",
            },
        "salary": {
            "type": "array",
            "items": {
                "anyOf": [{
                    "type": "integer",
                   },
                {
                    "type": "string",
                }]
            },
        }
    },
};

pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(jsonData, schema)).to.be.true;
});

//или (без первоначального парсинга response в переменную) + более распианные ошибки   

pm.test('Schema is valid', function() {
  pm.response.to.have.jsonSchema(schema);
});

```
_______________________________________________________________________

// пример построения теста сравнения   

``` js
pm.test("Текстовка", function () {
    pm.expect(jsonData.name).to.eql("Anna");
});
```

// сравнение  
``` js
.to.eql "="
```
``` js
.to.below "<"  
```
``` js
.to.above ">"
```

// ожидание  
``` js
pm.expect
``` 

// принадлежность к типу  
``` js
.to.be.a('number');
```

// наличие значения  
``` js
to.have.property
```

// статус в ответе 200 (например)    
``` js
pm.response.to.have.status(200)
```  

// вывод в консоль элемента по порядковому номеру  (из списка)  (в JSON это не сработает, т.к. JSON не нумеруем)  
``` js
console.log(jsonData.salary[0])
```

_______________________________________________________________________

**environment.set**  
**environment.get**

// Создать в окружении переменную name  
``` js
pm.environment.set("name");
```

// Создать в окружении переменную name и одновременно передать в нее переменную name из запроса URL  
``` js
pm.environment.set("name", req_url.name);
```  

//// получить из окружения переменную name  
``` js
pm.environment.get("name");
```

_______________________________________________________________________

// Написать цикл который выведет в консоль по порядку элементы списка из параметра salary. []-список  
``` js
var n = 0;
while (n < (jsonData.salary).length) 
{
console.log(jsonData.salary[n]);
n++
}
```


// Написать цикл который выведет в консоль по порядку элементы списка из параметра person. {}-JSON  

``` js
for (key in jsonData.person) {
    console.log( key + ": " + jsonData.person[key])
};
```

_______________________________________________________________________

// перевод в другой тип  
``` js
String(jsonData.age)
```

**Типы переменных JS**  
*String  
*Number  
*Object (JSON)  
*Boolean  

*null  
*undefined  
*symbol  
*BigInt  
__________________________________________________________________________
raw JSON   (Там где String "")
``` js
{
    "name":"{{name}}",
    "age":{{age}},
    "salary":1000,
    "auth_token":""
}
