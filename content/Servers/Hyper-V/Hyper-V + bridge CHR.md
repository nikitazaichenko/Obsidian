Если необходимо объединить локальные интерфейсы гипервизора в bridge на CHR, то на сетевом интерфейсе виртуальной машины CHR нужно включить MAC spoofing. В остальных случаях, если на интерфейсах будут использоваться разные IP адреса шлюза и не используется bridge, то подмена MAC адреса не нужна.

**Network Adapter** -- **Advanced Features** -- **Enable MAC address spoofing**

[![](https://sd.iservice.by/ru/file/kb_inline_image/ab9f727f5a7cdf49dfb99e8da83a7b8323237e1b)](https://sd.iservice.by/ru/file/kb_inline_image/ab9f727f5a7cdf49dfb99e8da83a7b8323237e1b)