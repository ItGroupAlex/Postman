# QA   
Текстовка заданий HW1/HW2/HW3: [QA_HW exercise 1-3.txt](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/HW_1-3_exercise.txt "link")   
Homework 1 and 2 (code): [HW1-2.postman_collection.json](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/HW1-2.postman_collection.json "link")  
Homework 1 and 2 (result of run): [HW1-2.postman_test_run.json](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/HW1-2.postman_test_run.json "link")   
Homework 3 (code): [HW3.postman_collection.json](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/HW3.postman_collection.json "link")  (without 5-6 ex. - don't work endpoints /curr_byn and /currency)  
Homework 3 (result of run): [HW3.postman_test_run.json](https://github.com/ItGroupAlex/Postman/blob/main/HW_QA/HW3.postman_test_run.json "link")   


Homework Charles:   
* [задание и ход выполнения](https://github.com/ItGroupAlex/Postman/blob/main/Charles/Charles_QA_HW.md "link")     
* [выгрузка из Charles](https://github.com/ItGroupAlex/Postman/blob/main/Charles/Charles_HW_export.chls "link")
* [выгрузка из Postman](https://github.com/ItGroupAlex/Postman/blob/main/Charles/Charles.postman_collection.json "link")   

Homework Fiddler:   
* [задание и ход выполнения](https://github.com/ItGroupAlex/Postman/blob/main/Fiddler/Fiddler_QA_HW.md "link")     
* [выгрузка из Fiddler](https://github.com/ItGroupAlex/Postman/blob/main/Fiddler/Rules_HW_fiddler.farx "link")
* [выгрузка из Postman](https://github.com/ItGroupAlex/Postman/blob/main/Fiddler/Fiddler.postman_collection.json "link")    


# Основные команды
// Спарсить response body в json.

`var jsonData = pm.response.json();`


// Спарсить request. (POST) (переменные в Body - form-data)

`var req = request.data`


// Спарсить request. (POST) (переменные в Body - raw(JSON))

`var req = JSON.parse(request.data);`

// Спарсить request.(GET)  
`var req_url = pm.request.url.query.toObject();`

// сравнение  
`eql "="`  
`below "<"`  
`above ">"`  


// pm.expect - ожидание

// пример построения теста

```
pm.test("Текстовка", function () {
    pm.expect(jsonData.name).to.eql("Anna");
});
```

// принадлежность к типу  
`.to.be.a('number');`

//вывод в консоль элемента по порядковому номеру  
`console.log(jsonData.salary[0])`
