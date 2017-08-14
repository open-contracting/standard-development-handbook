# OCDS Profiles

e.g. http://standard.open-contracting.org/profiles/ppp/latest/en/

# Copying live deploy into place

```bash
VER=1.0            # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
PROFILE=ppp        # (for example)

# Copy from dev3 to your local box
scp -r \
  root@dev3.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/${VER} \
  ${VER}-${DATE}-${SEQ}

# Copy from your local box to live2
scp -r \
  ${VER}-${DATE}-${SEQ} \
  root@live2.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/

# Symlink the version number
ssh root@live2.default.opendataservices.uk0.bigv.io \
  "rm /home/ocds-docs/web/profiles/${PROFILE}/${VER}; ln -sf ${VER}-${DATE}-${SEQ} /home/ocds-docs/web/profiles/${PROFILE}/${VER}"
```
