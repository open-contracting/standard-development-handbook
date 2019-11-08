# Open Contracting for Infrastructure Data Standards

[This profile](https://standard.open-contracting.org/infrastructure/latest/en/) is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting/infrastructure). It is [deployed](https://standard.open-contracting.org/infrastructure/) with the standard documentation. It was previously deployed to <https://open-contracting.github.io/infrastructure/>, which uses meta refresh to redirect to the current deployment.

## Development tasks

### Update blank.json

Install json-schema-random:

```shell
npm install git+https://github.com/open-contracting/json-schema-random.git
```

Update blank.json:

```shell
node_modules/json-schema-random/cli.js --no-random schema/project-level/project-schema.json > docs/examples/blank.json
```
