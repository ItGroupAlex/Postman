Charles HW Traffic capture

# Ex_0: 
Сфокусироваться на ниже перечисленных запросах

```
Protocol: http
IP: 162.55.220.72
Port: 5007
```

# Реализация задачи Ex_0:

Забиваем в Postman в Environments   
```
Protocol: http    
IP: 162.55.220.72   
Port: 5007
```

Создаем запрос
{{url}}/get_method?name=Alex&age=38   
посылаем запрос http://162.55.220.72:5007 и правой клавишей мыши выбираем "Focus"   

# Ex_1:   
```
Method: GET  
EndPoint: /get_method  
request url params:  
 name: str  
 age: int
```

response: 
```
[
    “Str”,
    “Str”
]
```

Task:
Сделать и в Rewrite, и в BreakPoint (можно отключить чтобы не стопило на каждом запросе)   
 ⁃ Подменить url в Charles чтобы в запросе ушло имя которые вы вписали в Postman, а вернулось то, которое вы подставили в Charles.   

# Реализация задачи Ex_1:

В Charles в BreakPoint выставляем перехват 162.55.220.72:5007 и меняем при необходимости запросы или ответы
В Rewrite выставляем автозамену в Rewrite, Modify Query Param:   
	Match - то что требует замены (Alex)   
	Raplace - то на что менять (Fedor)    
	обязательно указываем "name" переменной в Match и в Raplace (name)   

 Ex_2:
```
Method: POST
EndPoint: /user_info_3
request form data: 
 name: str
 age: int
 salary: int
```

response: 
```
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'u_salary_1_5_year': salary * 4}}
```

Task:
Сделать и в Rewrite, и в BreakPoint (можно отключить чтобы не стопило на каждом запросе)   
 ⁃ Подменить body в Charles так чтобы в запросе ушла salary которую вы вписали в Postman, а в u_salary_1_5_year цифра вернулась меньше оригинальной из запроса.

# Реализация задачи Ex_2:

В Charles в BreakPoint выставляем перехват 162.55.220.72:5007 Response и меняем u_salary_1_5_year в "Edit Response"
В Charles в Rewrite задаем BODY Response:   
	Match - то что требует замены ("u_salary_1_5_year":xxxx)   
	Raplace - то на что менять ("u_salary_1_5_year":zzzz)   
	
# Ex_3:
```
Method: GET
EndPoint: /object_info_1
request url params: 
 name: str
 age: int
 weight: int
```

response: 
```
{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}
```

Task:
Сделать и в Rewrite, и в BreakPoint (можно отключить чтобы не стопило на каждом запросе)
 ⁃ Подменить параметры запроса в Charles так, чтобы в Postman пришел ответ где другое name, daily_food > weight из запроса, а daily_sleep < weight из запроса.


# Реализация задачи Ex_3:
В Charles в BreakPoint выставляем перехват 162.55.220.72:5007 Response и меняем name / daily_food / daily_sleep в "Edit Response"    
В Charles в Rewrite задаем BODY Response:   
	Match - то что требует замены, например по  daily_food ("daily_food":xxxx)   
	Raplace - то на что менять ("daily_food":zzzz)  

# Ex_4:
```
Method: GET
EndPoint: /object_info_3
request url params: 
 name: str
 age: int
 salary: int
```

response: 
```
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'pets': {'cat':{'name':'Sunny',
                                     'age': 3},
                              'dog':{'name':'Luky',
                                     'age': 4}},
                     'u_salary_1_5_year': salary * 4}
          }
```

Task:
Сделать и в Rewrite, и в BreakPoint (можно отключить чтобы не стопило на каждом запросе)   
- Сделать через Charles так, чтобы сервер вернул 500 код.   
- Сделать через Charles так, чтобы сервер вернул 405 код.   

# Реализация задачи Ex_4:
В Charles в BreakPoint выставляем перехват 162.55.220.72:5007 Response и меняем 200 OK в "Edit Response" на 500 ОК / 405 ОК   
Назначаем в Rewrite для 162.55.220.72:5007/object_info_3 Response Status 500 вместо 200   
Назначаем в Rewrite для 162.55.220.72:5007/object_info_3 Response Status 405 вместо 200   

# Ex_5:
```
Method: GET
EndPoint: /object_info_4
request url params: 
 name: str
 age: int
 salary: int
```

response: 
```
{'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2), str(salary * 3)]}
```


Task:
Сделать и в Rewrite, и в BreakPoint (можно отключить чтобы не стопило на каждом запросе)   
 ⁃ Сделать через Charles так, чтобы сервер вернул 405 ошибку.   
 ⁃ Подменить salary в request   
 ⁃ Подменить (salary * 2) в response   

# Реализация задачи Ex_5:
* Назначаем в Rewrite для 162.55.220.72:5007/object_info_4 Response Status 405 вместо 200   
* В Charles в Rewrite задаем BODY request:    
	Match - то что требует замены ("salary":xxxx), например ("salary":2000)  
	Raplace - то на что менять ("salary":zzzz), например ("salary":10000)  
* В Charles в Rewrite задаем BODY response:   
	Match - то что требует замены (salary * 2) - ("salary":zzzz*2)  (20000)   
	Raplace - то на что менять ("salary":yyyy) , например ("salary":120000)   


# Ex_6:
```
Method: POST
EndPoint: /user_info_2
request form data: 
 name: str
 age: int
 salary: int
```

response: 
```
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }
```


Task:
Сделать и в Rewrite, и в BreakPoint (можно отключить чтобы не стопило на каждом запросе)   
 ⁃ Сделать через Charles так, чтобы в Postman вернулся ответ, в котором qa_salary_after_1.5_year переименовано в qa_salary_after_1.5_month   
 ⁃ Сделать так чтобы qa_salary_after_3.5_years было меньше qa_salary_after_12_months в response   

 # Реализация задачи Ex_6:
* В Charles в Rewrite задаем BODY response:    

	Match - то что требует замены (qa_salary_after_1.5_year)    
	Raplace - то на что менять (qa_salary_after_1.5_month)  

	Match - то что требует замены (7600)   
	Raplace - то на что менять (5000)   
