# HW2 Star Task Code
## http://162.55.220.72:5005/currency
Request:
```sh
POST
auth_token
```
Response:
```sh
[
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
…
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
]
```

## http://162.55.220.72:5005/curr_byn
Request:
```sh
POST
auth_token
curr_code: int
```
Response:
```sh
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}
```

## Задание:
1. получить список валют
2. итерировать список валют
3. в каждой итерации отправлять запрос на сервер для получения курса каждой валюты
4. если возвращается 500 код, переходим к следующей итреации
5. если получаем 200 код, проверяем response json на наличие поля `Cur_OfficialRate`
6. если поле есть, пишем в консоль инфу про фалюту в виде response
7. переходим к следующей итерации

## Решение:
```sh
let jsonData = pm.response.json();
let cur_id_list = [];

for (let count_list = 0; count_list < jsonData.length; count_list++) {
    cur_id_list.push(jsonData[count_list].Cur_ID)
};

for (let count = 0; count < cur_id_list.length; count++) {
    let post_info = {
        url: 'http://162.55.220.72:5005/curr_byn',
        method: 'POST',
        header: {
            'Content-Type': 'multipart/form-data',
        },
        body: {
            mode: 'formdata',
            formdata: [
                {key: "auth_token", value: pm.environment.get("token")},
                {key: "curr_code", value: cur_id_list[count]}
            ]
        },
    };
    pm.sendRequest(post_info, (error, response) => {
        if (response.code != 200) {
            // console.log('error');
        } else {
            let jsonData = response.json();
            console.log("Курс " + jsonData["Cur_Name"] + " - " + jsonData["Cur_OfficialRate"]);
        };
    });
};

```
## Пример результата:
```sh
22:48:08.895
Курс Филиппинских песо - 4.9275
 
22:48:08.896
POST http://162.55.220.72:5005/curr_byn
200
4.16 s
 
22:48:08.897
Курс Иранских риалов - 5.8262
 
22:48:08.898
POST http://162.55.220.72:5005/curr_byn
200
4.04 s
 
22:48:08.900
Курс Сомони - 2.2176
 
22:48:08.901
POST http://162.55.220.72:5005/curr_byn
200
4.18 s
 
22:48:08.903
Курс Тенге - 5.7475
 
22:48:08.904
POST http://162.55.220.72:5005/curr_byn
200
4.18 s
 
22:48:08.906
Курс Турецких лир - 2.6347
 
22:48:08.907
POST http://162.55.220.72:5005/curr_byn
200
4.04 s
 
22:48:08.908
Курс Шри-ланкийских рупий - 1.2584
```
