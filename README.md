# http_balancer
Homework for Practical Min  
**docker-compose build** - собрать  
**docker-compose up** - запустить 

**curl example:**  
Запишем с ключом hello и значением world:   
curl -X POST http://localhost:2000/put -i -d 'key="hello"&value=world'  
HTTP/1.0 200 OK

Взять запись по ключу:   
curl -X GET 'http://localhost:2000/get?key="hello"'   
{
  "from-cache": false, 
  "value": "world"
}

Запишем по ключу hello другое значение:  
curl -X POST http://localhost:2000/put -i -d 'key="hello"&value=UNEXPECTED'  
HTTP/1.0 200 OK

Взять запись по ключу: (достали старое значение)  
curl -X GET 'http://localhost:2000/get?key="hello"'  
{
  "from-cache": true, 
  "value": "world"
}

Взять запись по ключу с флагом no-cache:  
curl -X GET 'http://localhost:2000/get?key="hello"&no-cache=false'  
{
  "from-cache": false, 
  "value": "UNEXPECTED"
}

Удалить запись:  
curl -i -X DELETE 'http://localhost:2000/delete?key="hello"'  
HTTP/1.0 200 OK
