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

`var jsonData = pm.response.json();`


// Спарсить request. (POST) (переменные в Body - form-data)  

`var req = request.data`


// Спарсить request. (POST) (переменные в Body - raw(JSON))  

`var req = JSON.parse(request.data);`

//Спарсить request.(GET)  

`var req_url = pm.request.url.query.toObject();`

//проверка схемы JSON   

```
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

```
_______________________________________________________________________

// пример построения теста

```
pm.test("Текстовка", function () {
    pm.expect(jsonData.name).to.eql("Anna");
});
```

// сравнение  
`.to.eql` "="  
`.to.below` "<"  
`.to.above` ">"  

// ожидание  
`pm.expect` 

// принадлежность к типу  
`.to.be.a('number');`

// наличие значения  
`to.have.property`

// статус в ответе 200 (например)    
`pm.response.to.have.status(200)`  

// вывод в консоль элемента по порядковому номеру  (из списка)  (в JSON это не сработает, т.к. JSON не нумеруем)  
`console.log(jsonData.salary[0])`

_______________________________________________________________________

**environment.set**  
**environment.get**

// Создать в окружении переменную name  
`pm.environment.set("name");`

// Создать в окружении переменную name и одновременно передать в нее переменную name из запроса URL  
`pm.environment.set("name", req_url.name);`  

//// получить из окружения переменную name  
`pm.environment.get("name");`

_______________________________________________________________________

// Написать цикл который выведет в консоль по порядку элементы списка из параметра salary. []-список  
```
var n = 0;
while (n < (jsonData.salary).length) 
{
console.log(jsonData.salary[n]);
n++
}
```


// Написать цикл который выведет в консоль по порядку элементы списка из параметра person. {}-JSON  

```
for (key in jsonData.person) {
    console.log( key + ": " + jsonData.person[key])
};
```

_______________________________________________________________________

// перевод в другой тип  
`String(jsonData.age)`

**Типы переменных JS**  
*String  
*Number  
*Object (JSON)  
*Boolean  

*null  
*undefined  
*symbol  
*BigInt  
