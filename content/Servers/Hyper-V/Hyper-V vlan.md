Создаем объединение сетевых карт и необходимые интерфейсы с виланами на уровне хостовой ОС (см. соотвествующую документацию). Если Hyper-V поднят возможно перед созданием объединения будет необходимо убрать в свойствах физического сетевого адаптера птичку Hyper-V extensible virtual switch

[![](https://sd.iservice.by/ru/file/kb_inline_image/70123aa9a73a8a8b31ce51eeaebb1fabe349e0ed)](https://sd.iservice.by/ru/file/kb_inline_image/70123aa9a73a8a8b31ce51eeaebb1fabe349e0ed)

[![](https://sd.iservice.by/ru/file/kb_inline_image/02957a43987b9801d025383728de68e9b0619858)](https://sd.iservice.by/ru/file/kb_inline_image/02957a43987b9801d025383728de68e9b0619858)

После создания дополнительных интерфейсов они появляются  в свойствах виртуального коммутатора Hyper-V 

[![](https://sd.iservice.by/ru/file/kb_inline_image/b20eaf959d1aa7ced019bde8e4f0403072ab1375)](https://sd.iservice.by/ru/file/kb_inline_image/b20eaf959d1aa7ced019bde8e4f0403072ab1375)

выбираем необходимый. Для того, чтобы вилан был виден виртуальной машиной его надо дополнительно прописать в свойствах сетевой карты самой виртуальной машины

[![](https://sd.iservice.by/ru/file/kb_inline_image/0b752593272b9cd80120db84276bcaf7dbc0581d)](https://sd.iservice.by/ru/file/kb_inline_image/0b752593272b9cd80120db84276bcaf7dbc0581d)