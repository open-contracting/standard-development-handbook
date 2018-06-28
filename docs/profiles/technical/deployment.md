# Deployment

## Copying live deploy into place

See the [servers](../../../systems/servers) page for more info on how our servers are set up.

Set some variables (change the value of `PROFILE`):

```bash
VER=master         # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
PROFILE=root       # (for example)
```

Copy from dev server to your local box:

```bash
scp -r \
  root@dev3.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/${VER} \
  ${VER}-${DATE}-${SEQ}
```

Copy from your local box to the live server:

```bash
scp -r \
  ${VER}-${DATE}-${SEQ} \
  root@live2.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/
```

Symlink the version number:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io \
  "rm /home/ocds-docs/web/profiles/${PROFILE}/${VER}; ln -sf ${VER}-${DATE}-${SEQ} /home/ocds-docs/web/profiles/${PROFILE}/${VER}"
```
