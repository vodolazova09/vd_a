##### Мониторинг
**1.Статистика обращений к таблице**
Я создала базу данных и таблицу, заполнила её и удалила данные:
![avatar](https://sun9-45.userapi.com/impg/GebklqrE6DEaw-1oXNKPgmZKUv_r4LNcaFWqyg/r9JkWF-ehfk.jpg?size=570x245&quality=96&sign=82808e07417fd70b347299402f0cdc0c&type=album)
Проверила статистику обращений к таблице:
![avatar](https://sun9-77.userapi.com/impg/Y4WbBE9DcYZQ-YMIiGqvkJznywRTDYdy9FQO3w/5DnqoNt_rWk.jpg?size=599x374&quality=96&sign=e3fc6dae084e0a7e140e5451eeaf8361&type=album)
Из статистики следует, что было вставлено 1000 строк, удалено 1000 строк.
После этого не осталось активных версий строк.
Выполнила очистку и снова проверим статистику:
![avatar](https://sun9-42.userapi.com/impg/Rn4SFBlObyh6lEvtcQYP5G_Uar5GbagjyzqePQ/XVrkJd4erm8.jpg?size=592x410&quality=96&sign=22eb8e41a69b05f89fbf8d00ad1e70bf&type=album)
Неактуальные версии строк убраны при очистке, очистка обрабатывала таблицу один раз (vacuum_count = 1).
**2.Взаимоблокировка**
Создала ситуацию взаимоблокировки двух транзакций:
Одна транзакция блокирует первую строку таблицы
![avatar](https://sun9-40.userapi.com/impg/vnbmEP1ZCw3xhf518G4AyzaIKP1EjT2f50i9-Q/jjxXnaJ27Qc.jpg?size=444x95&quality=96&sign=f3784190621f079b6beca3ad0ddecaea&type=album)
Затем другая транзакция блокирует вторую строку
![avatar](https://sun9-88.userapi.com/impg/DJbEGwsiQM2DfV3g79iJOtsKcbFiPPHPHWIX4Q/NhQSsYqopOI.jpg?size=475x115&quality=96&sign=af4f0d6dd392354282e5a5a2c254c255&type=album)
Теперь первая транзакция пытается изменить вторую строку и ждет ее освобождения:
![avatar](https://sun9-75.userapi.com/impg/jbl237_mldIVZb-Xvh5YvW-2Q0OcC82hwTGotA/MsBwq79wbdE.jpg?size=427x87&quality=96&sign=fcf382d83aa6238a6a9ed93fcfcbe2a3&type=album)
Происходит взаимоблокировка.
Просмотрела журнал сообщений:
![avatar](https://sun9-16.userapi.com/impg/F7DbLXU9tlsafDTaBRI4CYrZQn3Z47mqYhoqEg/aftvcxaU10E.jpg?size=784x215&quality=96&sign=3ab93b498f30a0d3c5b9a7d84328d329&type=album)
**3.Расширение pg_stat_statements** 
Расширение собирает статистику планирования и выполнения всех запросов.
Для работы расширения требуется загрузить одноименный модуль. Для этого я прописала имя модуля в параметре shared_preload_libraries и перезагрузила серве:
![avatar](https://sun9-25.userapi.com/impg/l-KYyh2OMxxLDTWASoV7tUR28PIEmnnqvQ4zKg/HSxThoTpC2U.jpg?size=597x104&quality=96&sign=d0553da6115893328749f55a9807ef71&type=album)
![avatar](https://sun9-30.userapi.com/impg/haAvpafD22GvCu_cMGr28LlNzZH5FutbuoBGYA/dCQtwL4yGpc.jpg?size=444x162&quality=96&sign=5d601dee7cfc9cef89883654f7740d77&type=album)
Установила расштрение и выполнила несколько запросов:
![avatar](https://sun9-5.userapi.com/impg/MH9NZZ3B7FSjnqDxpob6xri0GWEf1gb8DnEGIA/ChPOsBKR7hk.jpg?size=530x247&quality=96&sign=15f4c0d9a96e27c33300aad8ee6ebb63&type=album)
Затем посмотрела статистику запроса, который выполнялся чаще всего:
![avatar](https://sun9-31.userapi.com/impg/az8ITN1DbmkBzCwnQv2_aTlDeAKci4e-R1Pkgw/uA6Q3mRnLrU.jpg?size=598x394&quality=96&sign=48f1794a6bd26e7176b9ec22e63b098a&type=album)



