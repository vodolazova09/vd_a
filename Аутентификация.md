При подключении клиента сервер должен идентифицировать пользователя, то есть определить его имя.
В целях выполнения данной лр я создала суперпользователя chesn:
![avatar](https://sun9-22.userapi.com/impg/X3mG8Veb78Qns6WhtopazTXUVlpFoOXBq2gmLg/txMQf4DQyao.jpg?size=659x155&quality=96&sign=1822954f99da628cc0b988addaf89f11&type=album)
Затем я сохранила файл pg_hba.conf, чтобы иметь возможность восстановить:
![avatar](https://sun9-48.userapi.com/impg/Gj2Lh1AwhlDx8jo3dIdxxbp32cuj4MJ79CnZaw/eOg8BLOOxHw.jpg?size=669x137&quality=96&sign=fdbda36e663acc56bc295f7bc80620c5&type=album)
Проверила содержимое файла pg_hba.conf  pg_hba.conf(используя представление pg_hba_file_rules):
![avatar](https://sun9-34.userapi.com/impg/HGpos8MoprP4E13dvh7T7hC7cE8wyIg4skii4w/m_arOk1bJds.jpg?size=612x295&quality=96&sign=8e0db70f6ba06197b87d951920fbf537&type=album)
Затем перезаписала pg_hba.conf с нуля:
![avatar](https://sun9-56.userapi.com/impg/glSOQ9sYs9az7fsqqhKPfpoSPo2ITCkSkzRANw/JP98bMObvBo.jpg?size=617x129&quality=96&sign=c588b8e27101789ec46d0df2375f4207&type=album)
Перезагрузила файл для сохранения настроек с помощью команды sudo pg_ctlcluster 12 main reload и просмотрела содержимое файла:
![avatar](https://sun9-87.userapi.com/impg/sM-iMdZKnTtSWRtnXOUO9vTNTz895SDc6LOfwg/kjSBJmUYqmw.jpg?size=674x214&quality=96&sign=e2096142be84ad3e83a0dd9090944317&type=album)
Проверила подключение. Подключилась как пользователь chesn к тестовой БД bd1:
![avatar](https://sun9-9.userapi.com/impg/nixEcX7pZkvTjXQChTs9xlIkARiVfn4Hq022Rg/c6iN3I32HC8.jpg?size=683x84&quality=96&sign=997e6b265db70d5fc17f6bd365b4d24e&type=album)
На снимке видно, что подключение прошло успешно.

