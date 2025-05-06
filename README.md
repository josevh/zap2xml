# zap2xml
Docker container for zap2xml. Forked from [shuaiscott/zap2xml](https://github.com/shuaiscott/zap2xml).

This is [zap2xml](https://web.archive.org/web/20200426004001/zap2xml.awardspace.info/) with environment variables driving the configuration. By default it runs every 12 hours to update your EPG data from zap2it. This container will take a second account for zap2it and will merge the received xml files into one using tv_merge.

## Compose
```yaml
---
services:
  zap2xml:
    image: ghcr.io/josevh/zap2xml
    container_name: zap2xml
    environment:
      - USERNAME=
      - PASSWORD=
      - OPT_ARGS=-I -D -a #optional
      - USERNAME2= #optional
      - PASSWORD2= #optional
      - OPT_ARGS2=-I -D #optional
      - XMLTV_FILENAME=xmltv.xml #optional
    volumes:
      - /path/to/xmltvdata:/data
    
```

## Docker CLI
```bash
docker run -d \
  --name zap2xml \
  -v /path/to/xmltvdata:/data \
  -e USERNAME="" \
  -e PASSWORD="" \
  -e OPT_ARGS="-I -D -a" `#optional` \
  -e USERNAME2= `#optional` \
  -e PASSWORD2= `#optional` \
  -e OPT_ARGS2="-I -D" `#optional` \
  -e XMLTV_FILENAME=xmltv.xml `#optional` \
  ghcr.io/josevh/zap2xml
```

## Parameters
>[!NOTE]
>Unless a parameter is flaged as 'optional', it is *mandatory* and a value must be provided.

| Parameter | Function |
| :-------: | -------- |
| `-e USERNAME=` | zap2it.com username |
| `-e PASSWORD=` | zap2it.com password |
| `-e OPT_ARGS=` | additional command line arguments for zap2xml |
| `-e USERNAME2=` | Second zap2it.com username |
| `-e PASSWORD2=` | Second zap2it.com password |
| `-e OPT_ARGS2=` | additional command line arguments for zap2xml for the second username |
| `-e XMLTV_FILENAME=` | filename for your xmltv file (default: xmltv.xml) |
| `-e SLEEPTIME=` | time in seconds to wait before next run (default: 43200) |
| `-v /path/to/xmltvdata:/data` | Contains xmltv files |