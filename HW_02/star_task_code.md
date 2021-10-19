# Star Task Code
```sh
let jsonData = pm.response.json();
let cur_id_list = [];

for (let count_list = 0; count_list < jsonData.length; count_list++) {
    // const items = jsonData[count_list]
    cur_id_list.push(jsonData[count_list].Cur_ID)
};
// console.log(cur_id_list);
// let currency_list_200 = [];

for (let count = 0; count < cur_id_list.length; count++) {
    let post_info = {  "url": "http://162.55.220.72:5005/curr_byn",
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
        log_list = [count, cur_id_list[count]]
        if (response.code != 200) {
            // pm.environment.set("Cur_ID", cur_id_list[count++]);
            // console.log('error', log_list);
        } else {
            let jsonData = response.json();
            // currency_list_200.push(jsonData);
            // pm.environment.set("Cur_ID", cur_id_list[count++]);
            // console.log('fine', log_list)
            console.log("Êóðñ " + jsonData["Cur_Name"] + " - " + jsonData["Cur_OfficialRate"]);
        };
    });
    // setTimeout(function() { console.log('sleep', count) }, 5000)
    // if (currency_list_200[count] != undefined) {
    //     console.log(currency_list_200[count]);
    // }
};
// console.log(currency_list_200);

```
Result example:
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
